AMWaveTransition
================

[![Build Status](https://travis-ci.org/andreamazz/AMWaveTransition.png)](https://travis-ci.org/andreamazz/AMWaveTransition)
[![Cocoapods](https://cocoapod-badges.herokuapp.com/v/AMWaveTransition/badge.png)](http://beta.cocoapods.org/?q=amwavetransition)
[![Analytics](https://ga-beacon.appspot.com/UA-42282237-8/AMWaveTransition/README)](https://github.com/igrigorik/ga-beacon)

Custom transition between viewcontrollers holding tableviews. Each cell is animated to simulate a 'wave effect'.

Screenshot
--------------------
![AMWaveTransition](https://raw.githubusercontent.com/andreamazz/AMWaveTransition/master/screenshot.gif)

Getting Started
=================

Install
--------------------
* Add ```pod 'AMWaveTransition'``` to your [Podfile](http://cocoapods.org/)
* Run ```pod install```
* Run ```open App.xcworkspace```

Setup as superclass
--------------------
* Subclass ```AMWaveViewController``` and override ```visibleCells``` or follow these steps:

Setup manually
--------------------
Implement ```UINavigationControllerDelegate``` and this delegate method:
```objc
- (id<UIViewControllerAnimatedTransitioning>)navigationController:(UINavigationController *)navigationController
                                  animationControllerForOperation:(UINavigationControllerOperation)operation
                                               fromViewController:(UIViewController*)fromVC
                                                 toViewController:(UIViewController*)toVC
{
    if (operation != UINavigationControllerOperationNone) {
        // Return your preferred transition operation
        return [AMWaveTransition transitionWithOperation:operation];
    }
    return nil;
}
```
Remember to set your instance as the navigation delegate:
```objc
- (void)viewDidAppear:(BOOL)animated
{
    [super viewDidAppear:animated];
    [self.navigationController setDelegate:self];
}

- (void)dealloc
{
    [self.navigationController setDelegate:nil];
}
```

Implement th ```AMWaveTransitioning``` protocol by returning your tableview's visible cells:
```objc
- (NSArray*)visibleCells
{
    return [self.tableView visibleCells];
}
```

As you can see in the sample project, the best results are obtained by setting the view and the cells' background to ```clearColor```, and setting a background color or a background image to the navigation controller.


Changelog 
==================

0.1
--------------------
- Initial release

TODO
==================
* Improve documentation

MIT License
--------------------
The MIT License (MIT)

Copyright (c) 2014 Andrea Mazzini

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.