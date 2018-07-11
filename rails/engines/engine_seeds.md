Question: how do i target a seeds.rb in an engine to avoid seeding my entire app?

Answer: [here](https://stackoverflow.com/a/51290476/1790307)


Edit the YOUR_ENGINE/lib/tasks/YOUR_ENGINE_tasks.rake

    namespace :db do
      namespace :YOUR_ENGINE do
        desc "loads all seeds in db/seeds.rb"
        task :seeds  => :environment do
          YOUR_ENGINE::Engine.load_seed
        end

        namespace :seed do
            Dir[Rails.root.join('YOUR_ENGINE', 'db', 'seeds', '*.rb')].each do |filename|
              task_name = File.basename(filename, '.rb')
              desc "Seed "      task_name      ", based on the file with the same name in `db/seeds/*.rb`"
              task task_name.to_sym => :environment do
                load(filename) if File.exist?(filename)
              end
            end
          end
      end
    end

then in your main app you can execute your custom seeds commands, executing any seed file individually

    $rake -T | grep YOUR_ENGINE
    rake db:YOUR_ENGINE:seed:seed1            # Seed seed1, based on the file with the same name in `db/seeds/*.rb`
    rake db:YOUR_ENGINE:seeds                 # loads all seeds in db/seeds.rb
