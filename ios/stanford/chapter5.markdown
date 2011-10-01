Chapter 5. Protocols and Views
===============================

Protocols
----------
Similar to @interface

no implementation
no instance

  @protocol Foo
  - (void) doSomething; // must implement
  @optional
  - (int) getSomething;
  @required
  - (NSArray *) getManySomethings:(int) howMany;// must
  @end

Foo.h

inside header file of another clss

classes then implement it
  @interface MyClass : NSObject <Foo>
    ...
  @end
  
  Can implement multiple protocol separated by comma.

  id <Foo> obj = [[MyClass alloc] init];// No compile error
  id <Foo> obj = [NSArray array]; //compile error or warning

Like generics... also can be specified in the arguments

  - (void) giveMeFooObject: (id <Foo>) anObjectImplementingFoo;



Just like static typing

only compiler helping stuff 

documentation of your method interfaces

uses in iOS
  delegate and dataSource

  @property (assign) id <UISomeObjectDelegate> delegate;
  

View
----

UIView


Rectangular area
draw and handle events inside that rectangle

Hierarchical
  one suerview (UIView)
  this is mostly constructed in Interface Builder

Possible to add View on code
  - (void) addSubview:(UIView *) aView;
  - (void) removeFromSuperview;

Manage order of subviews..


### View Transparency
views overlap

subviews index 0

hide a view
@property BOOl hidden;
myview.hidden = YES;

no events can be applied on hidden view.


## View Memory Management
superview retains its subviews

careful: remove view from hierarchy
get pointer it
retain it
then remove it

IBOutlets are retained
pointer to view in view hierarchy
they own for the safety reason

once super view released, then all child view released. So iOS trick for u... by retaining them...


Habit of releasing IBOutlets in right time

dealloc -> of controller

when controller will be dealloc the IBOutlet release

controller -> view
when all view reloaded
low memory situation... if views are off-screen


UIViewController ==> hooks
  - (void) viewDidLoad

  set attribute of IBOutlet which can't be done in Interface Builder

  - (void) viewDidUnload

  when view unloaded due to memory issue.


#### IBOutlet Memory Management

Create a property for each IBOutlet

  @property (retain) IBOutlet UILabel *display;
  1. usage of dot notation
  2. diclare as public API that IBOutlet is retained
  keep this in public. <header files>

  Interface Builder will call the setter.

  - (void) releaseOutlets {
    self.myOutlet = nil;
    self.myOtherOutlet = nil;
  }

  - (void) viewDidUnload {
    [self releaseOutlets];
  }

  - (void) dealloc {
    [self releaseOutlets];
    [super dealloc];
  }

27 min



























  


