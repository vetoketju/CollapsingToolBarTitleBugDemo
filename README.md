# CollapsingToolBarTitleBugDemo

Demoproject for a bug in Android Support Library 24.2.0:

- com.android.support:appcompat-v7:24.2.0
- com.android.support:design:24.2.0

Change between Build variants to see the difference.

Videos:
- [Bug 24.2.0](https://github.com/vetoketju/CollapsingToolBarTitleBugDemo/blob/master/buggy.mp4?raw=true)
- [Working 24.1.1](https://github.com/vetoketju/CollapsingToolBarTitleBugDemo/blob/master/working.mp4?raw=true)

## Bug

Expanding/collapsing title collapsed position is calculated wrong in onLayout() call of CollapsingToolbarLayout. If the view is not in its fully expanded position and onLayout gets called for example when adding a action item in the toolbar menu, then the collapsed position of the title will be too low. Changing the Collapsed- or ExpandedTitleGravities does not make any difference. The incorrect calcucation happens when CollapsingToolbarLayout is figuring out its offset to a dummyview it has added to the Toolbar. When it is calculating the position, ViewGroupUtils.offsetDescendantRect() is used. The implementation is different with android sdk ver >= 11, so < ver. 11 might not be affected. I think that the scrollY of the dummyview or collapsingtoolbar is not taken in to account, because the calculation is off by the same amount of AppBarLayouts vertical offset value.
