Adds a real-time traffic layer to your Mapbox basemap.

![trafficplugin](trafficplugin.gif)

## Getting Started with the Traffic Plugin

Once you have added the plugins library to your project, import it to your project. The traffic layers will start to become visible at zoom level 10.

These methods should not be called before [the style has finished loading](https://www.mapbox.com/ios-sdk/api/3.6.2/Protocols/MGLMapViewDelegate.html#/c:objc(pl)MGLMapViewDelegate(im)mapView:didFinishLoadingStyle:), which is the earliest opportunity to edit the map's style.

    - (void)addToMapView:(MGLMapView *)mapView;

Add traffic to a MGLMapView. This method inserts the traffic layer above the road layer. See the [Mapbox Vector Tile Source layer reference](https://www.mapbox.com/vector-tiles/mapbox-streets-v7/#layer-reference) for more information about vector tile layers.

    - (void)addToMapView:(MGLMapView *)mapView below:(MGLStyleLayer *)symbolLayer;

Insert the traffic layers below a specific layer that has already been added to your map’s style.

    - (void)removeFromMapView:(MGLMapView *)mapView;

Removes all traffic layers from the map.


## Examples

### Swift
```swift
    import Mapbox
    import MapboxPlugins

    class ViewController: UIViewController, MGLMapViewDelegate {

        override func viewDidLoad() {
            super.viewDidLoad()

            // This example is pinned to a style version because it accesses underlying style data.
            let mapView = MGLMapView(frame: view.bounds, styleURL: MGLStyle.lightStyleURL(withVersion: 9))
            mapView.setCenter(CLLocationCoordinate2D(latitude: 39.9612, longitude: -82.9988), zoomLevel: 11, animated: false)
            mapView.autoresizingMask = [.flexibleHeight, .flexibleWidth]
            view.addSubview(mapView)
            mapView.delegate = self
        }

        func mapView(_ mapView: MGLMapView, didFinishLoading style: MGLStyle) {
            let traffic = MBXTrafficPlugin()
            traffic.add(to: mapView)
        }
    }
```

### Objective-C

```objc
#import "ViewController.h"
#import <MapboxPlugins/MBXTrafficPlugin.h>

@interface ViewController () <MGLMapViewDelegate>

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view, typically from a nib.
    MGLMapView *mapView = [[MGLMapView alloc] initWithFrame: self.view.bounds styleURL:[MGLStyle lightStyleURLWithVersion:9]];
    [mapView setCenterCoordinate: CLLocationCoordinate2DMake(39.9612, -82.9988) zoomLevel:11 animated:NO];
    mapView.delegate = self;
    [self.view addSubview: mapView];
}

- (void)mapView:(MGLMapView *)mapView didFinishLoadingStyle:(MGLStyle *)style {
    MBXTrafficPlugin *traffic = [[MBXTrafficPlugin alloc] init];
    [traffic addToMapView:mapView];
}
```
