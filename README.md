Nexage Integration SourceKit for MRAID
======================================

[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
[![CocoaPods](https://img.shields.io/cocoapods/v/sourcekit-mraid-ios.svg)](https://github.com/MagicNarwhal/sourcekit-mraid-ios)

Nexage Integration SourceKit for MRAID is an easy to use library which implements the IAB MRAID 2.0 spec (http://www.iab.net/guidelines/508676/mobile_guidance/mraid). It is 
written in Objective-C and works in both iPhone and iPad applications.

**Features:**

- MRAID 2 implementation
- Handles full/fragment HTML
- 4 level logging
- Integrates with just a few lines of code
- ARC support

**Requirements:**

- iOS 8+
- Xcode: 8.1+
- SourceKitCommon Github project (https://github.com/nexage/sourcekit-common-ios) or Carthage build (https://github.com/HiddenJester/sourcekit-common-ios)

Getting Started
===============

Step 1: Set up your Cartfile to import sourcekit-mraid-ios & source-kit-common-ios like this:

	github "HiddenJester/sourcekit-mraid-ios" >= 1.0.7
	github "HiddenJester/sourcekit-common-ios" >= 1.0.4
	
Step 2: Configure carthage as per the instructions here: https://github.com/Carthage/Carthage

Step 3: Import sourcekit-mraid-ios into your project:

	@import sourcekitMRAID;
	
Step 4: Create an SKMRAIDView and add it to your container view, as in this example:

For a Banner:

     SKMRAIDView *bannerView = [[SKMRAIDView alloc] initWithFrame:CGRectMake(0, 0, 320, 50)
                                     withHtmlData:htmlData
                                      withBaseURL:bundleUrl
                                supportedFeatures:@[MRAIDSupportsSMS, MRAIDSupportsTel]
                                         delegate:self
                                  serviceDelegate:self
                               rootViewController:self];

    [self.view addSubview:bannerView];
   
**Note:** You must provide the creative content as a string along with a baseURL.  The 
creative may be either an HTML fragment or full HTML.

For an Interstitial:
	
		self.interstitial = [[SKMRAIDInterstitial alloc]
								initWithSupportedFeatures:@[MRAIDSupportsCalendar]
                                    		 withHtmlData:htmlData
                                              withBaseURL:bundleUrl
                                                 delegate:self
                                          serviceDelegate:self
                                       rootViewController:self];

	
Wait for the SKMRAIDInterstitialDelegate 'mraidInterstitialAdReady:' callback and do the following when the Ad is ready to be shown on screen:

	[mraidInterstitial show];
    
Inspect ad availabilith with [mraidInterstitial isAdReady] before you play the ad.

Step 5: (Optional) To see logging:
	
	@import SourceKitCommon.SKLogger;

	[SKLogger setLogLevel:SourceKitLogLevelDebug];   // select desired log level

Step 6: (Optional) Implement the SKMRAIDServiceDelegate Protocol if you wish to listen for and take action on MRAID calendar, storePicture, inlineVideo, and open browser events.

That's it! 


LICENSE
=======

Copyright (c) 2013, Nexage, Inc.<br/> 
All rights reserved.<br/>
Provided under BSD-3 license as follows:<br/>

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are
met:

1.  Redistributions of source code must retain the above copyright notice,
    this list of conditions and the following disclaimer.

2.  Redistributions in binary form must reproduce the above copyright
    notice, this list of conditions and the following disclaimer in the
    documentation and/or other materials provided with the distribution.

3.  Neither the name of Nexage nor the names of its
    contributors may be used to endorse or promote products derived from
    this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS
IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED
TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A
PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED
TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
