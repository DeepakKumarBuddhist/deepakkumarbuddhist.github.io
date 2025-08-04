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
}
