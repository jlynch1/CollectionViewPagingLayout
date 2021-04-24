# CollectionViewPagingLayout

[![License](https://img.shields.io/cocoapods/l/CollectionViewPagingLayout.svg?style=flat)](http://cocoapods.org/pods/CollectionViewPagingLayout)
![platforms](https://img.shields.io/badge/platforms-iOS-333333.svg)
[![pod](https://img.shields.io/cocoapods/v/CollectionViewPagingLayout.svg)](https://cocoapods.org/pods/CollectionViewPagingLayout)
[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage) 
[![Swift Package Manager compatible](https://img.shields.io/badge/Swift%20Package%20Manager-compatible-brightgreen.svg)](https://github.com/apple/swift-package-manager)

## Layout Designer
<img width="600" src="https://amir.app/git/layout_designer_preview.gif"></img>            
<a href="https://apps.apple.com/nl/app/layout-designer/id1507238011?l=en&mt=12"> <img width="100" src="http://amir.app/git/app_store.png"></img> </a>    


## Custom implementations

<p float="left">
<img width="100" src="https://amir.app/git/flowlayout_preview.gif"></img>
<img width="100" src="https://amir.app/git/gallery_preview.gif"></img>
<img width="100" src="https://amir.app/git/cards_preview.gif"></img>
</p>

### SnapshotTransformView

<p float="left">
<img width="100" src="https://amir.app/git/shapes_preview/snapshot_bars.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/snapshot_chess.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/snapshot_fade.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/snapshot_grid.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/snapshot_lines.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/snapshot_puzzle.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/snapshot_space.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/snapshot_tiles.gif"></img>
</p>

### ScaleTransformView
<p float="left">
<img width="100" src="https://amir.app/git/shapes_preview/scale_cylinder.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/scale_invertedcylinder.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/scale_linear.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/scale_easein.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/scale_easeout.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/scale_rotary.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/scale_coverflow.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/scale_blur.gif"></img>
</p>

### StackTransformView

<p float="left">
<img width="100" src="https://amir.app/git/shapes_preview/stack_blur.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/stack_perspective.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/stack_reverse.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/stack_rotary.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/stack_transparent.gif"></img>
<img width="100" src="https://amir.app/git/shapes_preview/stack_vortex.gif"></img>
</p>


## About
A simple but powerful framework that lets you make complex layouts for your `UICollectionView`.        
The implementation is quite simple. Just a custom `UICollectionViewLayout` that gives you the ability to apply transforms to the cells.       
No UICollectionView inheritance or anything like that.         
For more details, see [How to use](https://github.com/amirdew/CollectionViewPagingLayout#how-to-use)       


## Installation
This framework doesn't contain any external dependencies.

#### [CocoaPods](https://guides.cocoapods.org/using/using-cocoapods.html)

```ruby
# Podfile
use_frameworks!

target 'YOUR_TARGET_NAME' do
    pod 'CollectionViewPagingLayout'
end
```
Replace `YOUR_TARGET_NAME` and then, in the `Podfile` directory, type:

```bash
$ pod install
```

#### [Carthage](https://github.com/Carthage/Carthage)

Add this to `Cartfile`

```
github "CollectionViewPagingLayout"
```

and then, in the `Cartfile` directory, type:
```bash
$ carthage update
```

#### [Swift Package Manager](https://github.com/apple/swift-package-manager)

using Xcode:

File > Swift Packages > Add Package Dependency

#### Manually
Just add all the files under `Lib` directory to your project

## How to use

### Using Layout Designer
      
There is a macOS app to make it even easier for you to build your custom layout.            
It allows you to tweak many options and see the result in real-time.        
It also generates the code for you. So, you can copy it to your project.       

You can [purchase](https://apps.apple.com/nl/app/layout-designer/id1507238011?l=en&mt=1) the app from App Store and support this repository,
or you can build it yourself from the source.  
Yes, the macOS app is open-source too!. 


### Manually

- First, make sure you imported the framework
```swift
import CollectionViewPagingLayout
```
- Set up your `UICollectionView` as you always do (you need a custom class for cells)
- Set the layout for your collection view:
(in most cases you want a paging effect so enable that too)
```swift
let layout = CollectionViewPagingLayout()
collectionView.collectionViewLayout = layout
collectionView.isPagingEnabled = true // enabling paging effect
```

*Note:* Go to [Prepared Transformable Protocols](#prepared-transformable-protocols) if you want to use prepared effects! to make a custom effect contiune.   

- Now, you just need to conform your cell class to `TransformableView` and start implementing your custom transforms. 
for instance:
```swift
class YourCell: UICollectionViewCell { /*...*/ }
extension YourCell: TransformableView {
  func transform(progress: CGFloat) {
    // apply changes on any view of your cell
  }
}
```
As you see above, you get a `progress` value. Use that to apply any changes you want.  

> `progress` is a float value that represents the current position of your cell in the collection view.   
> When it's `0` that means the current position of the cell is exactly in the center of your collection view.   
> the value could be negative or positive and that represents the distance to the center of your collection view.   
> for instance `1` means the distance between the center of the cell and the center of your collection view is equal to your collection view width.


you can start with a simple transform like this:
```swift
extension YourCell: TransformableView {
    func transform(progress: CGFloat) {
        let transform = CGAffineTransform(translationX: bounds.width/2 * progress, y: 0)
        let alpha = 1 - abs(progress)

        contentView.subviews.forEach { $0.transform = transform }
        contentView.alpha = alpha
    }
}
```

- Don't forget to set `numberOfVisibleItems`, by default it's null and that means all of the cells will be loaded in the memory.  
```swift
layout.numberOfVisibleItems = ...
```

## Prepared Transformable Protocols

There are some prepared transformable protocols to make it easier to use this framework.             
Using them is simple. You only need to conform your `UICollectionViewCell` to the protocol.     
You can use the options property to tweak it as you want.         
There are three types:
- `ScaleTransformView` (orange previews) 
- `SnapshotTransformView` (green previews)
- `StackTransformView` (blue previews)     
These protocols are highly customizable, you can make tons of different effects using them.        
Here is a simple example for `ScaleTransformView` which gives you a simple paging with scaling effect:
```swift
extension YourCell: ScaleTransformView {
    var scaleOptions = ScaleTransformViewOptions(
        minScale: 0.6,
        scaleRatio: 0.4,
        translationRatio: CGPoint(x: 0.66, y: 0.2),
        maxTranslationRatio: CGPoint(x: 2, y: 0),
    )
}
```
There is an "options" property for each of these protocols where you can customize the effect, check the struct to find out what each parameter does.          
A short comment on the top of each parameter explains what that does.      
`ScaleTransformView` -> [`ScaleTransformViewOptions`](https://github.com/amirdew/CollectionViewPagingLayout/blob/master/Lib/Scale/ScaleTransformViewOptions.swift)     
`SnapshotTransformView` -> [`SnapshotTransformViewOptions`](https://github.com/amirdew/CollectionViewPagingLayout/blob/master/Lib/Snapshot/SnapshotTransformViewOptions.swift)     
`StackTransformView` -> [`StackTransformViewOptions`](https://github.com/amirdew/CollectionViewPagingLayout/blob/master/Lib/Stack/StackTransformViewOptions.swift)     
     
See the examples in the samples app.      
Check [here](https://github.com/amirdew/CollectionViewPagingLayout/tree/master/PagingLayoutSamples/Modules/Shapes/ShapeCell) to see used options for each: `/PagingLayoutSamples/Modules/Shapes/ShapeCell/`

#### Target view
You may wonder how does it find out the subview in your cell to apply transforms on.      
If you check the transformable protocols, you find the target view for each. like `ScaleTransformView.scalbleView`.      




The default value is the first subview of "contentView":
```swift
public extension ScaleTransformView where Self: UICollectionViewCell {
    
    /// Default `scalableView` for `UICollectionViewCell` is the first subview of
    /// `contentView` or the content view itself if there is no subview
    var scalableView: UIView {
        contentView.subviews.first ?? contentView
    }
}
```
If that's not what you want, you can implement it.


## Customize Prepared Transformables

Yes, you can customize them or even combine them.       
To do that, implement `TransformableView.transform` function and call the transformable function manually, like this:     
```swift
extension LayoutTypeCollectionViewCell: ScaleTransformView {
    
    func transform(progress: CGFloat) {
        applyScaleTransform(progress: progress)
        // customize views here, like this:
        titleLabel.alpha = 1 - abs(progress)
        subtitleLabel.alpha = titleLabel.alpha
    }

}
```
As you see, `applyScaleTransform` applies the scale transforms and right after that we change the alpha for `titleLabel` and `subtitleLabel`.        
To find the public function(s) of each protocol check the definition of that.      

## Other features

### Control current page

You can control the current page by the following functions of `CollectionViewPagingLayout`:
- `func setCurrentPage(_ page: Int, animated: Bool = true)`
- `func goToNextPage(animated: Bool = true)`
- `func goToPreviousPage(animated: Bool = true)`       

These are safe wrappers around setting the `ContentOffset` of `UICollectionview`.        
You can get the current page by a public variable `CollectionViewPagingLayout.currentPage`.    
Listen to the changes via `CollectionViewPagingLayout.delegate`:      
```swift
public protocol CollectionViewPagingLayoutDelegate: class {
    func onCurrentPageChanged(layout: CollectionViewPagingLayout, currentPage: Int)
}
```

### Select Item At

As explained in the Limitations, you can't use collectionview's didSelectItemAt for more than one cell.       
But, you can use this instead:      
- Implement `TransformableView.selectableView` and pass the view that you want to be selectable (by default it's the first subview of `UICollectionViewCell.contentView`)
- Call `layout.configureTapOnCollectionView()` AFTER setting the layout for you collection view.
- That's it. Now you get similar functionality by using `CollectionViewPagingLayout.delegate` instead of `CollectionView.delegate`
- The method is `func collectionViewPagingLayout(_ layout: CollectionViewPagingLayout, didSelectItemAt indexPath: IndexPath)`


## Limitations
-  Specify the number of visible cells:    

You need to specify the number of visible cells.       
Since this layout gives you the flexibility to show the next and previous cells,        
By default, it loads all of the cells in the collectionview's frame, which means iOS keeps all of them in the memory.      
Based on your design, you can specify the number of cells that you need to show.     

- didSelectItemAt:

The way that this library works is by putting all of the cells in the collectionview's frame and applying transforms on the target-view           
(`StackTransformView.cardView`, `ScaleTransformView.scalableView` and `SnapshotTransformView.targetView`).     

So, you can use `func collectionView(_ collectionView: UICollectionView, didSelectItemAt indexPath: IndexPath)` but if you have multiple cells on screen only one of them is selectable! (because the others are below it).          

You can implement `func zPosition(progress: CGFloat) -> Int` to specify which cell should be on the top.    

This also means you can't handle any gesture for multiple cells.        
But, there is a built-in solution to this, see [Select Item At](https://github.com/amirdew/CollectionViewPagingLayout#select-item-at)

- It doesn't support RTL layouts

## License

CollectionViewPagingLayout is available under the MIT license. See LICENSE file for more info.
