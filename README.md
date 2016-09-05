# HTML Canvas Gauges v2.0

[![Build Status](https://travis-ci.org/Mikhus/canv-gauge.svg?branch=v2.0.0)](https://travis-ci.org/Mikhus/canv-gauge) ![Test Coverage](https://rawgit.com/Mikhus/canv-gauge/v2.0.0/test-coverage.svg) ![Documentation Coverage](https://rawgit.com/Mikhus/canv-gauge/v2.0.0/docs-coverage.svg) [![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/Mikhus/canv-gauge/v2.0.0/LICENSE)

[![Canvas Gauges](https://raw.githubusercontent.com/Mikhus/blob/master/gauges.png)](https://rawgit.com/Mikhus/canv-gauge/v2.0.0/examples/component.html)

<!-- toc -->

- [Installation](#installation)
- [Using Gauges](#using-gauges)
  * [Configuration Options](#configuration-options)
    + [Common Configuration options](#common-configuration-options)
      - [Mandatory Options](#mandatory-options)
      - [Basic Options](#basic-options)
      - [Ticks Bar Options](#ticks-bar-options)
      - [Animation Options](#animation-options)
      - [Coloring Options](#coloring-options)
      - [Needle Configuration Options](#needle-configuration-options)
      - [Borders Options](#borders-options)
      - [Value Box Options](#value-box-options)
      - [Fonts Customization Options](#fonts-customization-options)
  * [Using As Components](#using-as-components)
  * [Scripting API](#scripting-api)
- [Sponsored By](#sponsored-by)
- [License](#license)

<!-- tocstop -->

This is tiny implementation of highly configurable gauge using pure JavaScript and HTML5 canvas.
No dependencies. Suitable for IoT devices because of minimum code base.

## Installation

Canvas gauges can be simply installed using npm package manager. Depending on your needs there is possibility to install whole gauge library or only that part you really need for your project.
To install the whole library, run:

    $ npm install canv-gauge

If you only need the exact type of the gauge it can be installed using the appropriate npm tag. Currently the following gauges are supported: linear, radial.

To install only linear gauge, run:

    $ npm install canv-gauge@linear

To install only radial gauge, run:

    $ npm install canv-gauge@radial

This strategy useful only if you need to minimize your code base and plan to use ONLY a specific gauge type. If you need to use various gauge types in your project it is recommended to use whole gauge package.

## Using Gauges

There are two ways inject gauges into your web-page:
 
 - as a web-component;
 - using JavaScript.

Whatever injecting type selected to use, first of all it is required to learn available gauge configuration options. Canvas gauges are **highly customizable controls**. You would be able to configure their look & feel at an extreme level of customization options. By the way to get a working gauge on your page it is possible to start with the zero-level of configuration.

### Configuration Options

Configuration options for the gauge usually passed to a constructor function and are a plain JavaScript object.

#### Common Configuration options

Common configuration options are spread across all type of the gauges means they are applicable to any gauge type. For been more informative and easy-to-find we split those options into groups below.

##### Mandatory Options

 - **renderTo**: render target in DOM tree. It is expected to be a canvas element or it's identifier in a DOM tree. This option is not required when the gauge injected as a web-component on the page.

##### Basic Options

 - **width**: number in pixels of the canvas element on which the gauge will be drawn.
 - **height**: number in pixels of the canvas element on which the gauge will be drawn.
 - **minValue**: numeric minimal value which will be shown on a gauge bar.
 - **maxValue**: numeric maximal value which will be shown on a gauge bar.
 - **value**: current gauge value which will be displayed.
 - **units**: should be a string explaining the units for the gauge value, or something falsy to hide this element on a gauge.
 - **glow**: boolean flag specifies if gauge should be drawn using glow effect or not.
 - **title**: should be a string to display gauge title or falsy value to hide this element.

##### Ticks Bar Options

Tick bars on a gauge representing the measuring system which visualize the gauge measuring intervals and the currently upset value. It should be upset in mind that ticks configuration must be relied properly on a given *minValue* and *maxValue* or you could get confusing display otherwise.

 - **majorTicks**: expected to be an array of numeric or string values which will be displayed on a gauge bar as major ticks.
  - **minorTicks**: is an integer number which defines how many minor ticks have to be drawn between two neighbour major ticks.
  - **strokeTicks**: boolean value defining if ticks bar of the gauge should be stroked or not. This relies only to a visual effect.
 - **majorTicksInt**: integer which defines how many numeric positions should be used to display integer part of the tick number.
 - **majorTicksDec**: integer which defines how many positions should be used to display decimal part of the tick number.
 - **highlights**: an array of highlights objects, which configures color-highlighted areas on a ticks bar. Each highlight object defines an area to colorize starting **from** value **to** value and using a given **color**, like this: ```{ from: number, to: number, color: string }```

##### Animation Options

Animations on the gauge can be turned on or off. Whenever the animation is turned on it will automatically run each time gauge changing it's value. During the animation gauge will animate its needle or progress bar from the old value to a new value it has been upset. If *animatedValue* option is turned on it will also constantly update the value displayed in a value box on each animation step.

 - **animation**: boolean flag signaling whenever the animation is possible on the gauge or not.
 - **animationDuration**: time in milliseconds of the animation duration.
 - **animationRule**: defines a type of animation behavior for the gauge. Canvas gauges already knows the most used types of animation rules or you can define your own animation rule providing the animation rule function within this option. Known rules could be bypassed as string names, which are: *"linear", "quad", "quint", "cycle", "bounce", "elastic"* and their opposites: *"dequad", "dequint", "decycle", "debounce", "delastic"*.
 - **animatedValue**: boolean flag specifies if a value displayed in a value box of the gauge should be constantly updated during animation run. By default it is falsy, so the upset gauge value will be shown immediately and animation will run visually only on the gauge needle or progress bar.

##### Coloring Options

Canvas gauge provides highly customizable coloring options for the majority of gauge elements. Each color configuration is usually a string value representing the color in one of HEX (#000000-#FFFFFF), RGB (rgb(0, 0, 0)-rgb(255,255,255)) or RGBA (rgba(0,0,0,0)-rgba(255,255,255,1)) formats. Some elements supports gradients. In this case the color of an element could be configured as color start and color end parts.

 - **colorPlate**: defines background color of the gauge plate.
 - **colorMajorTicks**: color of the major ticks lines (also applied to stroke if *strokeTicks* option is true). 
 - **colorMinorTicks**: color of the minor ticks lines.
 - **colorTitle**: color of the title text.
 - **colorUnits**: color of the units text.
 - **colorNumbers**: color of the text for the tick numbers.
 - **colorNeedle**: defines color of the gauge needle.
 - **colorNeedleEnd**: if defined it enables use of gradient for the gauge needle. If this is falsy, needle will be drown using solid color.
 - **colorValueText**: defines a color of the text in a value box.
 - **colorValueTextShadow**: defines a color of a text in a value box. If this value is falsy shadow won't be drawn.
 - **colorBorderShadow**: defines a shadow color of the gauge plate. If is falsy the shadow won't be drawn.
 - **colorBorderOuter**: defines a color of the outer border for the gauge plate.
 - **colorBorderOuterEnd**: if defined it enables use of gradient on the outer border.
 - **colorBorderMiddle**: defines a color of the middle border for the gauge plate.
 - **colorBorderMiddleEnd**: if defined it enables use of gradient on the middle border.
 - **colorBorderInner**: defines a color of the inner border for the gauge plate.
 - **colorBorderInnerEnd**:  if defined it enables use of gradient on the inner border.
 - **colorValueBoxRect**: defines a color of the value box rectangle stroke.
 - **colorValueBoxRectEnd**: if defined it enables use of gradient on value box rectangle stroke.
 - **colorValueBoxBackground**: defines background color for value box.
 - **colorValueBoxShadow**: defines a color of value box shadow. If falsy shadow won't be drawn.
 - **colorNeedleShadowUp**: defines upper half of the needle shadow color.
 - **colorNeedleShadowDown**: defines drop shadow needle color.

##### Needle Configuration Options

Gauge needle is an element which visualize the current position of the gauge value on a measuring bar. Currently canvas gauge supports drawing of two different types of the needles for each gauge - "line" needle and "arrow" needle. By the way, whenever it may be required, needle may be not drawn at all.

 - **needle**: boolean, specifies if gauge should draw the needle or not.
 - **needleShadow**: boolean, specifies if needle should drop shadow or not.
 - **needleType**: string, one of "arrow" or "line" supported.
 - **needleStart**: tail part of the needle length, in relative units.
 - **needleEnd**: main needle length in relative units.
 - **needleWidth**: max width of the needle in the most wide needle place.

##### Borders Options

Canvas gauge plate provides a way to define the borders. There are 3 borders availabe to draw on the edge of the gauge plate. It is possible to combine the borders display, their with and colors to achieve exclusive visual look & feel of your gauge.

 - **borders**: boolean, defines if a borders should be drawn or not.
 - **borderOuterWidth**: specifies a width in pixels of the outer border. If set to zero - border won't be drawn at all.
 - **borderMiddleWidth**: specifies a width in pixels of the middle border. If set to zero - border won't be drawn at all.
 - **borderInnerWidth**: specifies a width in pixels of the inner border. If set to zero - border won't be drawn at all.
 - **borderShadowWidth**: specifies the width of the outer border drop shadow. If zero - shadow won't be drawn.

##### Value Box Options

Value box element on the gauge is intended to display the digital representation of the current value. it is the most accurate visualisation of the exact value shawn by the gauge on the measuring bar. Whenever it is not required it may be turned off and not drawn.

 - **valueBox**: boolean, defines if the value box should be drawn or not on the gauge.
 - **valueBoxStroke**: number in relative units which defines the width of stroke of the value box element.
 - **valueText**: text to display instead of showing the current value. It may be useful when it is required to display something different in value box.
 - **valueTextShadow**: specifies if value text shadow should be drawn or not.
 - **valueBoxBorderRadius**: number of radius to draw rounded corners of the value box.
 - **valueInt**: integer which defines how many numeric positions should be used to display integer part of the value number.
 - **valueDec**: integer which defines how many positions should be used to display decimal part of the value number.
 
##### Fonts Customization Options

Canvas gauges enables use of custom fonts when drawing text elements. As far as gauges are build on principals of minimalistic code base there is no hardcoded fonts integrated with the gauges. Canvas gauges only provides a way to upset a custom font-family to its different text elements, but the font loading and initialization on the page is a part of the work user has to do himself.

 - **fontNumbers**: specifies font family for the tick numbers.
 - **fontTitle**: specifies font family for title text.
 - **fontUnits**: specifies font family for units text.
 - **fontValue**: specifies font-family for value box text.

### Using As Components

TBD

### Scripting API

TBD

## Sponsored By

[![Lohika](http://www.lohika.com/wp-content/themes/gridalicious/images/lohika_full.svg)](http://www.lohika.com/)

## License

This code is subject to [MIT](https://raw.githubusercontent.com/Mikhus/canv-gauge/v2.0.0/LICENSE) license.
