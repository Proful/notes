3. Objective-C and Foundation Frameworks
========================================
Instance Variable
------------------
16.30 min to 36.0 min
default: @protected
@private -> only class can access
@public -> anyone..
all variables @private
@property -> dot notation

  @interface MyObject : NSObject
  {
  @private
    int eye;
  }
  - (int) eye;// no argument
  - (void) setEye:(int) anInt;//set and capital letter
  //Instead of above 2 lines
  @property int eye;
  @end

  someObj.eye = newEyeValue;//set
  anotherEyeValue = someObj.eye;//get


@readonly
  @property (readonly) int eye;
can't set the value

@property does not have to match an instace variable name.
you don't have to declare the eye in interface.

But need to implemente in the implemeneation

  @implementation MyObject
  - (int) eye{
    return eye;  
  }
  - (void) setEye: (int) anInt {
    eye = anInt;  
  }
  // above two not re
  @synthesize eye 
  @end


After synthesize also you can implemente any setter and getter method. that will take precedence.  

  //Infinite loop
  - (void) setEye:(int) anInt
  {
    self.eye = anInt;  
  }

properties?

safety
match c struct
C also has dot notation for struct
C struct same as object but don't have function. carry data around...

magic...
  @interface MyObject()
  @property double myEyesOnly;
  @end

36 min to 44 min : Demo
changed the long declaration in calculator example to dot notation.
Understanding dot notation will really helps.

Dynamic Binding
----------------
44 min to 
all object are allocated in heap. so always use pointers

Never use "id *" -> a pointer to a pointer to an object
decision at run time
NSString *s = ...;
id new_s = s;
both the code generated exactly same. only compile time checking only.

cast a pointer (legal and some time useful)
id obj = ...;
NSString *str = (NSString *) obj;


### Object Typing
  @interface Vehicle
  - (void) move;
  @end
  @interface Ship : Vehicle
  - (void) shoot;
  @end
  Ship *s = [[Ship alloc] init];
  [s shoot];
  [s move];

  Vehicle *v = s;
  [v shoot];//compile warning...

  id obj = ...;
  [obj shoot];//no compile warning... 
  [obj someJunkMethod];// compiler will warn

  NSString *hello = @"hello";
  [hello shoot];// compile warning
  
  Ship *helloShip = (Ship *)hello;
  [helloShip shoot];//compile fine.. but runtime error

  [(id)hello shoot];//compile fine. but runtime error

### Introspection
54 min..
NSObject

isKindOfClass: obj of class (+ inheritance)
isMemberOfClass: obj of class (- inheritance)
respondsToSelector: obj responds to the method

  if( [obj isKindOfClass:[NSString class]] ){
     //cast and logic 
  }


@selector
  if( [obj respondsToSelector:@selector(shoot)]){
    //cast and logic
  }

SEL objective C "type"

SEL shootSelector = @selector(shoot);

### nil
59 min..
value of object pointer that does not point to anything.
like zero in the primitive types int, double etc

NSObject makes all the instance variable to zero
  if(obj){
    // will execute if obj is not nil
  }

Important:
Sending messages to nil is okay!!!! no code gets executed
int i = [obj methodReturnInt];//i = 0 if obj is nil

Careful:-
CGPoint p = [obj getLocation];//in this case CGPoint is C Struct
                              //p will be undefined...

### BOOL
1hr 01 min
YES -> true
NO -> false
NO == 0, YES everything else

Foundation Framework
---------------------
1hr 02 min
### NSObject
- (NSString *) description

### NSString
Unicode
@"foo"
immutable -- cannot be modified
send a message to NSString and it will return a new one
returning a string

### NSMutableString
can modified
inside loop

### NSNumber
wrapper for int, float,double etc
NSNumber *num = [NSNumber numberWithFloat:36.5]
float f = [num floatValue]

### NSValue
wrapper for non-object data types
c struct

### NSData
generic untyped data
image
html page
lot of api available and straight forward
char * or byte *

### NSDate
date now, store date in fs
NSCalender






