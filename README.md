# Flutter JSON from file

This example loads a sample dataset from a file and displays a random entry in the UI


## Loading data from a static json file

Register the file in the assets section of pubspec.yaml

```yaml
assets:
  - assets/data/quotes.json
```

Import Services and convert

```dart
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
```

Load data into a variable

```dart
class _MyHomePageState extends State<MyHomePage> {
  List _quotes = [];
  

  @override
  void initState() {
    readJson();
    
    super.initState();
  }
...

  void readJson() async {
    final String response =
        await rootBundle.loadString('assets/data/quotes.json');
    final data = await json.decode(response);

    setState(() {
      _quotes = data;
    });
  }
```

Display a random quote

```dart
class Quote {
  String quote = "";
  String author = "";
}
class _MyHomePageState extends State<MyHomePage> {
  List _quotes = [];
  Quote qod = Quote();

  @override
  void initState() {
    readJson();
  
    super.initState();
  }
...
  


  void _getRandomQuote() {
    if (_quotes.length > 0) {
      int index = Random().nextInt(_quotes.length);
      Quote q = Quote()
        ..author = _quotes[index]["author"]
        ..quote = _quotes[index]["quote"];

      setState(() {
        qod = q;
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    _getRandomQuote();

...

  Text(qod.quote),


```

Pull a new quote

```dart


  ...

     floatingActionButton: FloatingActionButton(
        onPressed: _getRandomQuote,
        tooltip: 'Refresh',
        child: const Icon(Icons.refresh),
      ),

  ...

```
