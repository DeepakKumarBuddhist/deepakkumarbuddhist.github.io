# deepakkumarbuddhist.github.io
यह वेबसाइट दीपक कुमार द्वारा समाज सेवा और बौद्ध विचारधारा के प्रचार-प्रसार के लिए बनाई गई है। इसमें उनके कार्यों, अनुभवों और सामाजिक कार्यक्रमों की जानकारी दी गई है।
import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';
import 'dart:io';
import 'package:firebase_core/firebase_core.dart';
import 'package:firebase_storage/firebase_storage.dart';
import 'package:cloud_firestore/cloud_firestore.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MaterialApp(home: DataForm()));
}

class DataForm extends StatefulWidget {
  @override
  _DataFormState createState() => _DataFormState();
}

class _DataFormState extends State<DataForm> {
  File? _image;
  final picker = ImagePicker();

  final TextEditingController nameController = TextEditingController();
  final TextEditingController emailController = TextEditingController();
  final TextEditingController fatherController = TextEditingController();
  final TextEditingController villageController = TextEditingController();
  final TextEditingController mobileController = TextEditingController();

  Future pickImage() async {
    final pickedFile = await picker.pickImage(source: ImageSource.gallery);
    setState(() {
      _image = File(pickedFile!.path);
    });
  }

  Future uploadData() async {
    String? imageUrl;
    if (_image != null) {
      final storageRef = FirebaseStorage.instance
          .ref()
          .child("user_photos/${DateTime.now().millisecondsSinceEpoch}");
      await storageRef.putFile(_image!);
      imageUrl = await storageRef.getDownloadURL();
    }

    await FirebaseFirestore.instance.collection("userData").add({
      "name": nameController.text,
      "email": emailController.text,
      "fatherName": fatherController.text,
      "village": villageController.text,
      "mobile": mobileController.text,
      "photoUrl": imageUrl ?? "",
      "timestamp": FieldValue.serverTimestamp()
    });

    ScaffoldMessenger.of(context).showSnackBar(SnackBar(content: Text("Data Uploaded")));
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("User Info Upload")),
      body: SingleChildScrollView(
        padding: EdgeInsets.all(16),
        child: Column(
          children: [
            ElevatedButton(onPressed: pickImage, child: Text("Pick Photo")),
            if (_image != null) Image.file(_image!, height: 100),
            TextField(controller: nameController, decoration: InputDecoration(labelText: "Name")),
            TextField(controller: emailController, decoration: InputDecoration(labelText: "Email")),
            TextField(controller: fatherController, decoration: InputDecoration(labelText: "Father's Name")),
            TextField(controller: villageController, decoration: InputDecoration(labelText: "Village Name")),
            TextField(controller: mobileController, decoration: InputDecoration(labelText: "Mobile Number")),
            SizedBox(height: 20),
            ElevatedButton(onPressed: uploadData, child: Text("Upload Data"))
          ],
        ),
      ),
    );
  }
}dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^latest
  firebase_storage: ^latest
  cloud_firestore: ^latest
  image_picker: ^latest# 📲 Flutter User Info Upload App

यह एक मोबाइल ऐप है जो यूज़र से निम्न जानकारी लेकर Firebase पर सुरक्षित करता है:
- 📷 फ़ोटो अपलोड
- 🙋 नाम
- 📧 ईमेल
- 👨‍👦 पिता का नाम
- 🏡 गाँव का नाम
- 📱 मोबाइल नंबर

## 🔧 तकनीकी स्टैक

| Layer        | Tool           |
|--------------|----------------|
| Frontend     | Flutter        |
| Backend      | Firebase       |
| Storage      | Firebase Storage (Image) |
| Database     | Cloud Firestore|

## 🚀 फीचर्स

- सरल और responsive UI
- Firebase Storage में इमेज अपलोड
- Firestore में structured data सेव
- टाइमस्टैम्प के साथ ट्रैकिंग

## 🛠️ सेटअप गाइड

### 1. Flutter प्रोजेक्ट रन करें

```bash
flutter pub get
flutter run
