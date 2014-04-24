# Objective-C style guide.

This style guide outlines the coding conventions of the iOS team at Intelex, LLC.

## Table of Contents

* [Commenting](#commenting)
* [Organization](#organization)
* [Spacing](#spacing)
* [Indent Style](#indent_style)
* [Variables](#variables)
* [Methods](#methods)
* [Properties](#properties)
* [Private Properties](#private-properties)
* [Dot-notation Syntax](#dot-notation-syntax)
* [Literals](#literals)
* [Constants](#constants)
* [Enumeration](#enumeration)
* [Booleans](#booleans)
* [Init](#init)
* [Singletons](#singletons)

##Commenting

* Comments should be used to organize your code and to provide extra information for future refactoring or for other developers who will be reading your code.

**Example**

```objC
// This is an inline comment

/* This is a block comment 
with multiple lines. */
```

##Organization

* Using `#pragma mark` to organize your code.

```objC
#pragma mark - Init

- (instancetype)init
{
}
		
- (void)viewDidLoad
{
}

#pragma mark - IBActions

- (IBAction)useForce:(id)sender
{
}
```

##Spacing

* Xcode defaults to 4 spaces, so to increase the likelihood of consistency, use 4 spaces.

##Indent Style

* Allman style is preferred for functions. K&R C indent style is preferred for **if** and **for** blocks inside a function, however, have their opening braces at the same line as their respective control statements; closing braces remain in a line of their own, unless followed by an else or while keyword.

**Example**

```objC
@implementation SomeClassName
	
- (BOOL)checkPresent
{
	for (Wookiee *wookiee in wookieesList) {
		// some code
	}
}
@end
```

##Variables

* Variables should be named as descriptively as possible.

* Asterisks indicating pointers belong with the variable.

**Example**

```objC
// Good
NSString *personName = @"Obi-Wan Kenobi";
	
// Bad
NSString * personName = @"Jabba the Hutt";
		
// Bad
NSString* personName = @"Darth Vader";
```

##Methods

* In method signatures, there should be a space after the scope (-/+ symbol). There should be a space between the method segments.

**Example**

```objC
// Good
- (void)setName:(NSString *)name forImage:(UIImage *)image;
		
// Bad
-(void)set:(NSString *)n i:(UIImage*)img;
```

##Properties

* Property attributes should be explicitly listed, and will help new programmers when reading the code. The order of properties should be storage then atomicity, which is consistent with automatically generated code when connecting UI elements from Interface Builder.

```objC
// Good
@property (weak, nonatomic) IBOutlet UIView *loadView;
@property (strong, nonatomic) NSString *jediName;
		
// Bad
@property(nonatomic,weak) IBOutlet UIView *loadView;
@property (nonatomic) NSString *title;
```

##Private Properties

* Private properties should be declared in class extensions (anonymous categories) in the implementation file of a class.

**Example**

```objC
@interface YASomeViewController ()
		
@property (strong, nonatomic) UIView *thumbsView;
@property (strong, nonatomic) UIWebView *webView;
		
@end
```

##Dot-notation Syntax

* Dot syntax is purely a convenient wrapper around accessor method calls. When you use dot syntax, the property is still accessed or changed using getter and setter methods. Read more here. Dot-notation should always be used for accessing and mutating properties, as it makes code more concise. Bracket notation is preferred in all other instances.

**Example**

```objC
// Good
view.backgroundColor = [UIColor whiteColor];
[UIApplication sharedApplication].delegate;
		
// Bad
[view setBackgroundColor:[UIColor whiteColor]];
UIApplication.sharedApplication.delegate;
```

##Literals

* NSString, NSNumber, NSArray, and NSDictionary literals should be used whenever possible.

```objC
NSString *jediName = @"Luke";
NSNumber *starshipSpeed = @160;
NSArray *deathStars = @[@"Star #1", @"Star #2"];
NSDictionary *driver = @{@"name": @"Han Solo", @"force" : @1};
```

##Constants

* Constants should be declared as static constants and not #defines unless explicitly being used as a macro.

```objC
// Good
static NSString * const YATitleName = @"Story Title";
static CGFloat const YADefaultHeight = 230.0;
		
// Bad
#define TitleName @"Story Title"
#define defaultHeight 2.0
```

##Enumeration

* An enum should be defined using NS_ENUM and bitmasks should be defined using NS_OPTIONS. The enum or bitmask should be named using the project prefix

**Example**

```objC
// enum
typedef NS_ENUM(NSInteger, XYStarshipType) {
	XYStarshipFighter,
	XYStarshipCargo,
	XYStarshipSpy
};
		
// bitmask
typedef NS_OPTIONS(NSInteger, XYCollisionCategory) {
	XYCollisionCategoryCar,
	XYCollisionCategoryWall,
	XYCollisionCategoryBuilding,
	XYCollisionCategoryPerson
};
		
// Untyped with a name
typedef enum {
	UIElementStyleDefault,
	UIElementStyleOne,
	UIElemrntStyleTwo,
	UIElemrntStyleThree
} UIElementStyle;
```

##Booleans

* Objective-C uses YES and NO. Therefore true and false should only be used for CoreFoundation, C or C++ code. Since nil resolves to NO it is unnecessary to compare it in conditions. Never compare something directly to YES, because YES is defined to 1 and a BOOL can be up to 8 bits.

```objC
// Good
if (someObject) {
}
		
if (![anotherObject boolValue]) {
}
		
// Bad
if (someObject == nil) {
}
		
if ([anotherObject boolValue] == NO) {
}
		
if (isAwesome == YES) {
}
		
if (isAwesome == true) {
}
```

##Init

* Init methods should follow the convention provided by Apple's generated code template. A return type of 'instancetype' should also be used instead of 'id'.

```objC
- (instancetype)init 
{
	self = [super init];
		  
	if (self) {
		// ...
	}
	return self;
}
```

##Singletons

* Singleton objects should use a thread-safe pattern for creating their shared instance.

```objC
+ (instancetype)sharedInstance 
{
	static dispatch_once_t onceToken = 0;
	static id sharedInstance = nil;
		
	dispatch_once(&onceToken, ^{
		sharedInstance = [[self alloc] init];
	});
		
	return sharedInstance;
}
```
