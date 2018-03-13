Question: Add icon to ion-option in ion-select

Answer: [here](https://stackoverflow.com/questions/44119567/add-icon-to-ion-option-in-ion-select/49266549#49266549)

[![enter image description here][1]][1]


  [1]: https://i.stack.imgur.com/GyTug.png

This worked for me.

using CSS to modify the inner span in the button tag of each option, removing radius and assigning a brackground image

the options keep the same order, and that is why the attribute selector worked for me

    .alert-radio-icon{
        border-radius: 0 !important;
        border: none !important;
        height: 40px !important;
        width: 40px !important;
        background-size: 40px 40px !important;
        background-repeat: no-repeat ;
    }

    [id^="alert-input-"][id$="-0"] .alert-radio-icon{
        background-image: url("../assets/images/menu/flag_ni.png") !important;
    }
    [id^="alert-input-"][id$="-1"] .alert-radio-icon{
        background-image: url("../assets/images/menu/flag_gt.png") !important;
    }
    .alert-radio-inner{
        background-color: transparent !important;
    }