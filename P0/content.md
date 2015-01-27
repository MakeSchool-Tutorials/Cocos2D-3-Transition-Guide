---            
title: Cocos2D a Brief Transition Guide
slug: coco2d-brief-tranistion-guide
---

For this tutorial post we assume you are already familiar with Cocos2d 2.x. We will point out the important changes that come with the new version of Cocos and give example implementations based on what you already know from Cocos2d 2.x.

#   CCNodes, CCScenes and CCLayers

CCLayer does not exist anymore. CCLayer used to be the class you used for scenes with user interaction. In Cocos2d 3.x any CCNode can handle touch input. *CCNode is the new CCLayer*. For scenes use CCScene for everything in your scene use CCNode.

#   Touch handling

We will soon come up with a complete tutorial on touch handling in Cocos2d 3.0. For now it is most important to know how:

*   to enable touch handling on you CCNode:

    	self.userInteractionEnabled = TRUE;

*   to catch a touch and its touch position:

	    - (void)touchBegan:(UITouch *)touch withEvent:(UIEvent *)event
	    {
	         CGPoint touchLocation = [touch locationInNode:self]; 
	         // put your touch handling code here
	    }

*   And to know the three other methods that can be implemented to determine moving, ending, or canceled touches:

	    - (void)touchMoved:(UITouch *)touch withEvent:(UIEvent *)event
	    - (void)touchEnded:(UITouch *)touch withEvent:(UIEvent *)event
	    - (void)touchCancelled:(UITouch *)touch withEvent:(UIEvent *)event

## Note for Cocos2D 3.3

If you are using Cocos2D 3.3+ (it's part of SpriteBuilder 1.3+) you will have to replace all occurrences of *UITouch* and *UITouchEvent* with *CCTouch* and *CCTouchEvent*, respectively. You can find more information as part of the [SpriteBuilder update guide](http://www.spritebuilder.com/update).

# Good bye CCMenu! Hello CCLayout!

In the past CCMenu was the easiest way to create a menu. Since CCMenu was the only class that provided handy layout methods (alignItemsVertically, etc.) the class was often used to layout a lot of other things, not only menus. Cocos2d 3.0 solves this issue by providing a CCLayout class. This class can layout any kind of CCNode, which makes layouting our scenes a charm. If you want to build a menu in Cocos2d 3.0 you will use a CCLayout container and simply add CCButtons to it. This is an example from a simple layout:

    // create first button
    self.calculationStepButton = [CCButton buttonWithTitle:LABEL_STEP];
    [self.calculationStepButton setTarget:self selector:@selector(calculationStepButtonTouched:)];
    // create second button
    self.animationButton = [CCButton buttonWithTitle:LABEL_ANIMATE];
    [self.animationButton setTarget:self selector:@selector(animateButtonTouched:)];
    // setup layoutbox and add items
    CCLayoutBox *layoutBox = [[CCLayoutBox alloc] init];
    layoutBox.anchorPoint = ccp(0.5, 0.5);
    [layoutBox addChild:self.calculationStepButton];
    [layoutBox addChild:self.animationButton];
    layoutBox.spacing = 10.f;
    layoutBox.direction = CCLayoutBoxDirectionVertical;
    [layoutBox layout];
    layoutBox.position = ccp(CANVAS_SIZE.width + (self.contentSize.width - CANVAS_SIZE.width)/2, self.contentSize.height/2);
    [self addChild:layoutBox];

# Implementing a custom update Method

In Cocos2d 2.x you needed two steps in order to implement an update method that is called every frame:

    // 1) schedule update 
    [self scheduleUpdate]; 
    ... 
    // 2) override update method
    - (void) update:(ccTime)delta 
    {
        ... 
    }

In Cocos 2d 3.x you do not need to call scheduleUpdate anymore. Instead you only override this method in any CCNode subclass:

    - (void)update:(CCTime)delta {
           ...
    }

# There's more to come!

In the coming days and weeks we will be adding many tutorials on new Cocos2d 3.0 APIs, so stay tuned.

If you're missing any instructions for Cocos2d 3.0 please shoot me an E-Mail: benji@makegameswith.us
