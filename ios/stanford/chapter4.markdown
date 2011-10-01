4. Foundation(Array,Dictionaries), Memory
=========================================

### NSArray
ordered list of object
immutable -- no addition or removal of object

  - (int) count
  - (id) objectAtIndex: (int) index;
  - (id) lastObject; //return nil if no object

### NSMutableArray
  - (void) addObject

### NSDictionary
immutable
key value pair
key must implement
  - (NSUInteger) hash
  - (BOOL) isEqual: (NSObject *) obj
key ==> NSString
important method
  - (int) count
  - (id) objectForKey:(id)key
  - (NSArray *) allKeys
  - (NSArray *) allValues

### NSMutableDictionary
  - (void) setObject:(id)anObject forKey: (id)key
  - (void) removeObjectForKey:(id) key

### NSSet
unordered collection of obect
all object needs to be unique
immutable
  - (int) count
  - (BOOL) containsObject:(id)anObject
  - (id) anyObject

### NSMutableSet


Enumeration 
--------------

  NSArray *myArray = ...;
  for (NSString *string in myArray) {
    double value = [string doubleValue];  
  }


  NSSet *mySet = ...;
  for id obj in mySet){
    if([obj isKindOfClass:[NSString class]]){
      //do something  
    }
      
  }

  NSDictionary *myDictionary = ...;
  for (id key in myDictionary) {
    id value = [myDictionary objectForKey:key];
  }

Property List
--------------

collection of collections

NSArray, NSDictionary, NSNumber, NSString, NSDate, NSData

why???

iOS SDK uses this in some api

NSUserDefaults
---------------

Light weight storage of property list
preferences

R/W via standardUser Defaults

setter /getter methods..

Creating Objects
----------------

Allocating -> alloc (NSObject)
Initialization -> init

do alloc and init should be in one line...

alloc
  makes space in heap for the class's instance variables

init
  every class should have initializer
  NSObject -> init
  subclass need to over-ride init

  MyObject *obj = [[MyObject alloc] init];


  @implementation MyObject
  - (id) init
  {
    if([super init]) {
      // Initialize our subclass here
      return self;
    } else {
      return nil;
    }  
  }
  @end

  UIView
  - (id) initWithFrame:(CGRect) aRect;


### Getting Objects
alloc/init is not the only way to get the object

  NSString *newDisplay = [display.text stringByAppendingString:digit];
  NSArray *keys = [dictionary allKeys];

who frees the memory??
No garbage collection..
not in iOS... gc availabel in Mac



Reference Counting
-------------------
Take ownership for an object you want to keep a pointer to

once u done.. give up that ownership

when no one claims ownership.. it gets deallocated

### Object Ownership
new, alloc or copy
if you specify the above 3 keyword.. you own

what if u don't own object created using the above 3 object. but some one given to you
  retain

Giveup the ownership
  release
  don't send release twice... hard to find bug

### Temporary Ownership
  autorelease

ownership expire after some time.

  - (Money *) showMeTheMoney:(double) amount{
    Money *theMoney = [[Money alloc] init:amount];
    //here we can't release bcoz we want to release the object
    [theMoney autorelease];
    return theMoney;
  }

  Money *myMoney = [bank showMeTheMoney:4500.00];
  [myMoney retain];



  //need to autorelease
  NSMutableArray *returnValue = [[NSMutableArray alloc] init];
  //no need for autorelease
  NSMutableArray *returnValue = [NSMutableArray array];

There are lots of autorelease method.

If you put any object in the collection. That's collection class responbility to retain and release it. They own it.

@"string" => autoreleased
but they r not autoreleased.. they r constant

NSString copy rather than retain
that gives immutable version


release an object as soon as possible
 --> code readability

### Deallocation

last owner calls release
special method dealloc

you should override "dealloc" in your classes
but never NEVER call it

in the dealloc method
release the instance method...

it will be called when the object is released by the owner.

Once one place you can call dealloc
inside the subclass dealloc call super's dealloc


  - (void) dealloc
  {
    [brain release];
    [super dealloc];
  }


### @property

getter => return instance variables directly
usually caller don't release it
it will assume it is autorelease..

if caller.. retains then only it will release it.

  display.text = [display.text stringByAppendingString:digit];

  didn't take ownership of display.text
  I created a new string by appnding digit

setter method:-
@synthesize do the setting for u

following option

  @property (retain) NSArray *myArrayProperty;
  @property (copy) NSString *someNameProperty;
  @property (assign) NSString *someNameProperty;


Demo
----
collects object string and number
report statistics

Model: Collector
View: Bunch of random buttons
Controller: CollectorViewController

NSNumber to wrap primitive








































