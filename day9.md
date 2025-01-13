## Day 9 
# 메모장 앱 만들기

```dart
import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Memo App',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        colorSchemeSeed: Colors.blue,
      ),
      home: const MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({
    super.key,
  });

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  final List<String> _notes = ['Hello', 'Good morning'];
  final TextEditingController _controller = TextEditingController();
  
  void _addNote() {
    String text = _controller.text;
    
    if (text.isNotEmpty) {
      setState(() {
        _notes.add(text);
        print(_notes);
        _controller.clear();  
      });
    }
  }
  
  void _deleteNote(int index) {
    setState(() {
      _notes.removeAt(index);    
    });
  }
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Memo App"),
      ),
      body: Column(
        children: <Widget>[
          Expanded(
            child: ListView.builder(
              itemCount: _notes.length,
              itemBuilder: (context, index) {
                return Card(
                  child: ListTile(
                    title: Text(_notes[index]),
                    trailing: IconButton(
                      onPressed: () => _deleteNote(index),
                      icon: const Icon(Icons.delete),
                    )
                  )
                );
              }
            )
          ),
          Padding(
            padding: const EdgeInsets.all(8.0),
            child: Row(
              children: <Widget>[
                Expanded(
                  child: TextField(
                    controller: _controller,
                    decoration: const InputDecoration(hintText: 'Input your memo')
                  )
                ),
                IconButton(
                  onPressed: _addNote,
                  icon: const Icon(Icons.save),
                )
              ]
            )
          )
        ]
      ),
    );
  }
}

```