# deepakkumarbuddhist.github.io
यह वेबसाइट दीपक कुमार द्वारा समाज सेवा और बौद्ध विचारधारा के प्रचार-प्रसार के लिए बनाई गई है। इसमें उनके कार्यों, अनुभवों और सामाजिक कार्यक्रमों की जानकारी दी गई है।

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
