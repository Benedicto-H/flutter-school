## Day 10
# 메모장 앱 더 만들기

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
        _controller.clear();
      });
    }
  }

  void _deleteNote(int index) {
    setState(() {
      _notes.removeAt(index);
    });
  }

  void _navigateToEditNote(int index) async {
    // Get the current note text
    String currentNote = _notes[index];

    // Navigate to the edit note page
    final editedNote = await Navigator.push(
      context,
      MaterialPageRoute(
        builder: (context) => EditNotePage(currentNote: currentNote),
      ),
    );

    // Update the note if modified
    if (editedNote != null) {
      setState(() {
        _notes[index] = editedNote;
      });
    }
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
                    trailing: Row(
                      mainAxisSize: MainAxisSize.min,
                      children: [
                        IconButton(
                          onPressed: () => _navigateToEditNote(index),
                          icon: const Icon(Icons.edit),
                        ),
                        IconButton(
                          onPressed: () => _deleteNote(index),
                          icon: const Icon(Icons.delete),
                        ),
                      ],
                    ),
                  ),
                );
              },
            ),
          ),
          Padding(
            padding: const EdgeInsets.all(8.0),
            child: Row(
              children: <Widget>[
                Expanded(
                  child: TextField(
                    controller: _controller,
                    decoration: const InputDecoration(hintText: 'Input your memo'),
                  ),
                ),
                IconButton(
                  onPressed: _addNote,
                  icon: const Icon(Icons.save),
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }
}

class EditNotePage extends StatefulWidget {
  final String currentNote;

  const EditNotePage({super.key, required this.currentNote});

  @override
  State<EditNotePage> createState() => _EditNotePageState();
}

class _EditNotePageState extends State<EditNotePage> {
  final TextEditingController _controller = TextEditingController();

  @override
  void initState() {
    super.initState();
    _controller.text = widget.currentNote;
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Edit Note"),
      ),
      body: Padding(
        padding: const EdgeInsets.all(8.0),
        child: Column(
          children: [
            TextField(
              controller: _controller,
              decoration: const InputDecoration(hintText: 'Edit your memo'),
              maxLines: null, // Allow multiline editing
            ),
            ElevatedButton(
              onPressed: () {
                Navigator.pop(context, _controller.text); // Pop with edited text
              },
              child: const Text("Save"),
            ),
          ],
        ),
      ),
    );
  }
}
```