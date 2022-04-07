# CardiOp
A framework to let developers easily connect their iPhones, iPads or Mac to CardiOp app on the Apple Watch to receive realtime Heart Rate

*Requirements*

*  iOS 13, macOS 10.15
* Swift 5.5+
* Xcode 13.0+

*Installation*

The preferred way of installing CardiOp is via the Swift Package Manager 

1. In Xcode, open your project and navigate to *File* -> *Swift Packages* -> *Add Package Dependency*…
2. Paste the repository URL (https://github.com/bredventures/CardiOp.git) and click *Next*
3. For Rules, select *Branch* ( with branch set to `master` )
4. Click *Finish*

*Usage*

Using the CardiOp framework is straightforward

1. `import CardiOpFramework`
2.  Create an instance of CardiOpServices by calling
```
 var cardiOpService = CardiOpServices.shared
```
3. When you are ready to start the pairing between CardiOp Apple Watch app and your iOS device, conform to the `cardioDelegate` and  call `connect`
```
cardiOpService.cardiopDelegate = self
cardiOpService.connect()
```
4. The delegate callbacks are designed to send you information about the connection, any UI messages and the Heart Rate itself
```
public protocol CardioPServicesDelegate {
    // Any UI updates that needs to be shown on the equipment
    func uiUpdates(message: String)
    // The Heart Rate update
    func updateHR(value: String)
    // Call back when the equipment successfully connects to the Apple Watch app
    func didConnectToCentral()
    // Failure callback when the connection fails with the reason for failure
    func didFailToConnectToCentral(reason: String)
}
```
5. When you are ready to start the workout from the equipment call the following
`sendWorkoutStatus(started: started, type: type, location: location)`
/Started/ :  Indicates if the workout started or ended
/type/: Pass in the type of workout activity using HKWorkoutActivityType
/location/: Pass in the location type using HKWorkoutSessionLocationType
