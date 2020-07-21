# Foloosi Payment

[![pub package](https://img.shields.io/pub/v/foloosi_flutter_payment.svg)](https://pub.dev/packages/foloosi_flutter_payment)

A Flutter plugin for making payments via Foloosi Payment Gateway. Fully supports Android and iOS.

<div style="text-align: center">
    <table>
        <tr>
            <td style="text-align: center">
                <img src="https://raw.githubusercontent.com/FoloosiTech/foloosi_flutter_payment/master/sample.gif" width="400" />
            </td>
        </tr>
    </table>
</div>

## Installation

In the `dependencies:` section of your `pubspec.yaml`, add the following line:

```yaml
foloosi_flutter_payment: ^1.0.1
```

Import in your project:
```dart
import 'package:foloosi_flutter_payment/foloosi_flutter_payment.dart';
```

## Basic Usage
```dart
class MyHomePage extends StatefulWidget {
  MyHomePage({Key key}) : super(key: key);

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {

final GlobalKey<ScaffoldState> _scaffoldKey = new GlobalKey<ScaffoldState>();

bool proceedToPayment = false;

  void _proceeedToPayment() {
    setState(() {
      proceedToPayment = true;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      key: _scaffoldKey,
      appBar: proceedToPayment
          ? null
          : AppBar(
              title: Text('Foloosi Payment Flutter'),
            ),
      body: proceedToPayment
          ? FoloosiPayment(
              headerText: 'Foloosi Payment',
              successRoute: '/OrderSuccess',
              successRouteParam: 'Foloosi',
              loaderText: "Processing Request",
              merchantKey: 'YOUR_FOLOOSI_MERCHANT_KEY',
              secretKey: 'YOUR_FOLOOSI_SECRET_KEY',
              transactionAmount: 2000,
              currency: 'AED',
              customerName: 'Omar Ali',
              customerEmail: 'tech@foloosi.com',
              customerMobile: '+971000000000',
              onError: (value) {
                print("Payment Error : $value");
                setState(() {
                  proceedToPayment = false;
                });
                _scaffoldKey.currentState.showSnackBar(SnackBar(
                  content: Text(value.toString()),
                  duration: Duration(seconds: 3),
                ));
              },
              onSuccess: (value) {
                print("Payment Success : $value");
                setState(() {
                  proceedToPayment = false;
                });
                _scaffoldKey.currentState.showSnackBar(SnackBar(
                  content: Text(value.toString()),
                  duration: Duration(seconds: 3),
                ));
              },
            )
          : Center(
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: <Widget>[
                  RaisedButton(
                    onPressed: _proceeedToPayment,
                    child: new Text(
                      "Proceed to Payment",
                    ),
                  )
                ],
              ),
            ),
    );
  }
}
```

Note: If you're using the foloosi secret and merchant keys as a string in flutter, remember to escape the $ dollar signs although it is recommended to load these from your backend
```markdown
merchantKey: 'YOUR_MERCHANT_KEY',
secretKey: 'YOUR_SECRET_KEY',
```

## Properties

Here is a list of properties available:

|        Name        	    |       Type      |     Required	  |                 Description                	              |
|:------------------:	    |:---------------:|	:---------------: |:---------------------------------------------------------:|
| headerText         	    | String          |	    false         | the title of the widget's appbar           	              |
| onError           	    | Function        |	    true          | function to run on payment error              	          |
| onSuccess         	    | Function        |	    true          | function to run on payment success            	          |
| loaderText         	    | String          |	    false         | text to display under the loader               	          |
| merchantKey               | String          |	    true          | your foloosi merchant key                      	          |
| secretKey                 | String          |	    true          | your foloosi secret key                       	          |
| referenceToken            | String          |	    false         | the reference token - generates automatically if null     |
| redirectUrl               | String          |	    false         | the redirect url                                          |
| transactionAmount         | String          |	      -           | transaction amount - required if referenceToken is null   |
| currency                  | String          |	      -           | transaction currency - required if referenceToken is null |
| customerName              | String          |	    false         | customer name - auto render in payment popup if passed    |
| customerEmail             | String          |	    false         | customer email - auto render in payment popup if passed   |
| customerMobile            | String          |	    false         | customer mobile - auto render in payment popup if passed  |
| customerAddress           | String          |	    false         | customer address - auto render in payment popup if passed |
| customerCity              | String          |	    false         | customer city - auto render in payment popup if passed    |
| paymentCancellationMsg    | String          |	    false         | message returned when user cancels the payment            |
| debugMode                 | bool            |	    false         | to enable or disable package logs                         |


## Developed  by

```
Foloosi
```

## License

Copyrights (c) 2020 Foloosi