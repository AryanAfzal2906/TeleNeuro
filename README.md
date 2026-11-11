# 🧠 TeleNeuro

<p align="center">
  <b>AI-Powered Telemedicine Platform for Early Alzheimer's Detection</b><br/>
  <i>Alzheimer Disease Detection Using Vision Transformers and MRI Images</i><br/>
  Joint Final Year Project (BS Computer Science, Session 2022–2026) — University of Engineering and Technology (UET), Taxila
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Flutter-3.x-02569B?logo=flutter&logoColor=white" />
  <img src="https://img.shields.io/badge/Firebase-Auth%20%7C%20Firestore-FFCA28?logo=firebase&logoColor=black" />
  <img src="https://img.shields.io/badge/Supabase-Storage-3ECF8E?logo=supabase&logoColor=white" />
  <img src="https://img.shields.io/badge/AI%20Model-ViT--B%2F16-orange" />
  <img src="https://img.shields.io/badge/Accuracy-99.37%25-brightgreen" />
  <img src="https://img.shields.io/badge/Platform-Android-3DDC84?logo=android&logoColor=white" />
  <img src="https://img.shields.io/badge/Project-FYP-blueviolet" />
  <img src="https://img.shields.io/badge/License-MIT-green" />
</p>

---

## 📖 Overview

**TeleNeuro** is a full-stack Flutter telemedicine application that connects **patients** and **neurologists**, combined with an **on-device AI diagnostic engine** for early Alzheimer's detection from brain MRI scans.

The app runs a fine-tuned **Vision Transformer (ViT-B/16)** model — converted to TFLite and bundled directly into the app — so MRI classification happens **entirely on-device**, without sending medical images to any external inference server.

Patients can upload an MRI scan, receive an instant AI-generated diagnosis report (PDF), book appointments with doctors, chat in real time, and securely share their reports — all within one app.

> **🎓 Joint Final Year Project** — Developed by **Aryan Afzal** and **Malik Anas Ahmed** at the Department of Computer Science, UET Taxila, under the supervision of **Dr. Rabbia Mahum**. See [Team & Contributions](#-team--contributions) for who built what.

---

## 👥 Team & Contributions

| | Aryan Afzal | Malik Anas Ahmed |
|---|---|---|
| **Registration No.** | UET/22-CS-89 | UET/22-CS-150 |
| **Role** | AI & Backend Lead | Mobile Application Lead |
| **GitHub** | [@AryanAfzal2906](https://github.com/AryanAfzal2906) | — |

### 🤖 Aryan Afzal — AI & Backend Lead
- **Dataset engineering:** merged the Kaggle Alzheimer's MRI dataset with the OASIS Brain MRI dataset (~120,000 augmented images across 4 classes), cleaned corrupted files and built the 80/20 train/test split.
- **Preprocessing pipeline:** designed the Resize(256) → CenterCrop(192) → Grayscale→RGB → Resize(224) → ImageNet normalization pipeline, plus rotation (±10°) and affine (5% shift) augmentation. Horizontal flips were intentionally avoided because they can create false structural features in brain MRI.
- **Model development:** fine-tuned **ViT-B/16** (PyTorch/torchvision) with a custom classification head (Dropout 0.5 + Linear), AdamW (lr 2e-5, weight decay 0.2), label smoothing (0.2), mixed-precision (AMP) training, gradient clipping and early stopping on a Tesla T4 GPU.
- **Model comparison:** trained and evaluated ViT, Swin Transformer and ConvNeXt, then selected the best-performing model.
- **Model evaluation:** achieved **99.37% accuracy** and a weighted F1-score of 0.99 on an independent cross-dataset holdout of 1,279 unseen MRI images.
- **Mobile deployment pipeline:** exported the trained model PyTorch → ONNX → TFLite and validated that the converted model keeps the original diagnostic accuracy.
- **Backend configuration:** server-side setup and database integration support for the cloud services.

### 📱 Malik Anas Ahmed — Mobile App & Cloud Integration Lead
- Designed and developed the cross-platform Flutter UI/UX for both the Patient and Doctor portals.
- Implemented MRI image selection, local preprocessing and state management inside the app.
- Integrated the on-device TFLite model into the app (UI ↔ inference engine).
- Implemented Firebase Authentication with role-based access control (Patient vs Doctor).
- Configured Firestore for real-time chat, appointments and notifications.
- Built the structured PDF report generation and Supabase storage integration.
- Led system and user acceptance testing (UAT) of the mobile workflows.

### 🤝 Shared work
Requirements analysis, system design (use case, activity, sequence, class and architecture diagrams), integration of the AI model with the app, testing and the final FYP report.

---

## ✨ Features

### 👤 Patient Side
- Secure sign-up / login (Gmail-restricted email validation, 18+ age gate)
- Browse & search doctors by specialization, sorted by rating
- Book appointments with date/time picker + problem description
- Real-time chat with doctors after appointment acceptance
- **AI MRI Diagnosis** — upload a scan, get instant stage classification + confidence score (results below 80% confidence are rejected as unreliable)
- Auto-generated PDF diagnostic report, saved to personal **Lab Reports** library
- Share MRI reports selectively with doctors (only those with an accepted appointment)
- In-app notifications (bookings, messages, session updates, shared reports)
- Editable profile with photo upload (Supabase-backed)
- Secure account deletion with password re-authentication

### 🩺 Doctor Side
- Separate doctor registration flow (specialization, qualification, hospital, experience)
- Dashboard with live stats: total patients, pending requests, rating, experience
- Accept / decline appointment requests in real time
- Dedicated chat inbox per patient, with "End Session" and delete conversation controls
- View shared MRI reports & clinical summaries from linked patients
- "My Patients" directory built from appointment history
- Patient reviews & ratings section on public profile
- In-app doctor guide / FAQ

### 🔐 Shared / Core
- Dual-role authentication routing (Patient vs Doctor) via Firestore role checks
- Firestore-backed real-time notification engine (deduplicated per event)
- Appointment-scoped chat with visibility rules (auto-hides chat if either account is deleted)
- Reusable UI kit: searchable dropdowns, animated buttons, custom date pickers, badge icons

---

## 📸 Screenshots

| Patient Dashboard | MRI Reports | Appointments |
|:---:|:---:|:---:|
| <img width="720" height="1600" alt="patient_dashboard" src="https://github.com/user-attachments/assets/e080490f-6c75-419e-91db-5a8c7b3b6280" /> | <img width="720" height="1600" alt="Reports" src="https://github.com/user-attachments/assets/d52293f2-6f84-4055-96b2-4eda3eb73b47" /> | <img width="720" height="1600" alt="Appointments" src="https://github.com/user-attachments/assets/976fe406-76fa-4b53-bb63-7a609427aa40" /> |

| Doctor Dashboard | Doctor Profile | User Guide |
|:---:|:---:|:---:|
| <img width="720" height="1600" alt="doctor_dashboard" src="https://github.com/user-attachments/assets/e186770d-218d-4e5b-bc04-e49d1aa5920b" /> | <img width="720" height="1600" alt="doctor_profile" src="https://github.com/user-attachments/assets/8404a1ed-0edf-4494-92da-3cf95df4dcba" /> | <img width="720" height="1600" alt="user_guide" src="https://github.com/user-attachments/assets/f7b59a0b-f0b0-4b5f-9f00-ac6fbe145afa" /> |

---

## 🧠 AI Model

| | |
|---|---|
| **Architecture** | Vision Transformer — `ViT-B/16` (torchvision, ImageNet-pretrained) |
| **Task** | 4-class classification: `NonDemented`, `VeryMildDemented`, `MildDemented`, `ModerateDemented` |
| **Training framework** | PyTorch (mixed-precision / AMP, gradient clipping, early stopping) |
| **Optimizer / Loss** | AdamW (lr 2e-5, weight decay 0.2) / CrossEntropy with label smoothing 0.2 |
| **Batch size / Epochs** | 64 / max 50 (early stopping, patience 5) |
| **Hardware** | NVIDIA Tesla T4 (Kaggle) |
| **Datasets** | [Alzheimer's MRI Dataset](https://www.kaggle.com/datasets/aryanafzal/alzheimers-mri-dataset) + [OASIS Brain MRI Dataset](https://www.kaggle.com/datasets/ninadaithal/imagesoasis) (~120,000 augmented images, 80/20 split) |
| **Export pipeline** | PyTorch → ONNX (opset 14) → TFLite (via `ai-edge-torch`) |
| **On-device runtime** | `tflite_flutter` |
| **Input** | `224×224×3` RGB tensor, ImageNet-normalized |

**Preprocessing pipeline (must match training exactly):**
Resize(256) → CenterCrop(192) → Grayscale→RGB → Resize(224) → Normalize(ImageNet mean/std) → CHW

### 📊 Results (cross-dataset holdout, 1,279 unseen MRI images)

| Class | Precision | Recall | F1-Score | Support |
|---|:---:|:---:|:---:|:---:|
| MildDemented | 1.00 | 1.00 | 1.00 | 179 |
| ModerateDemented | 1.00 | 1.00 | 1.00 | 12 |
| NonDemented | 1.00 | 0.99 | 0.99 | 640 |
| VeryMildDemented | 0.99 | 1.00 | 0.99 | 448 |
| **Overall accuracy** | | | **99.37%** | 1,279 |

The only notable confusion is between `NonDemented` and `VeryMildDemented`, the two most clinically similar stages.

The full training/export notebook is documented in `final-fyp.ipynb`.

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Flutter (Dart) |
| Authentication | Firebase Auth |
| Database | Cloud Firestore (real-time) |
| File Storage | Supabase Storage (MRI PDFs, images, profile photos) |
| AI Training | PyTorch, torchvision, timm (Kaggle GPU) |
| AI Inference | TensorFlow Lite (on-device) |
| PDF Generation | `pdf` package |
| State/Local Cache | `shared_preferences` |

---

## 📂 Project Structure

```
lib/
├── Splash/                       # Onboarding / splash screens
├── Profile Side/                 # Role selection (Patient / Doctor)
├── Patient Side/
│   ├── Auth/                     # Patient login, signup, portal
│   ├── Screens/                  # Dashboard, appointments, chat, MRI upload, reports...
│   └── services/                 # MRI report service
├── Doctor Side/
│   ├── Auth/                     # Doctor login, signup, portal
│   ├── Screens/                  # Dashboard, appointments, chat, patients, reports...
│   └── Widgets/                  # Doctor-specific cards
├── Widgets/                      # Shared reusable widgets (avatars, dropdowns, pickers...)
├── services/                     # Shared services (auth, notifications, validation...)
├── data/                         # Static option lists (specializations, qualifications)
├── firebase_options.dart
├── supabase_config.dart
└── main.dart

assets/
├── screen1.png ... screen4.jpg   # Onboarding illustrations
└── vit_fyp_direct.tflite         # AI model (NOT committed — see setup below)
```

---

## 🚀 Getting Started

### Prerequisites
- Flutter SDK `^3.9.2`
- A Firebase project (Auth + Firestore enabled)
- A Supabase project (Storage bucket)

### 1. Clone the repository
```bash
git clone https://github.com/AryanAfzal2906/teleneuro.git
cd teleneuro
```

### 2. Install dependencies
```bash
flutter pub get
```

### 3. Configure Firebase
- Create a Firebase project → enable **Email/Password Auth** and **Firestore**.
- Run:
```bash
flutterfire configure
```
  This regenerates `lib/firebase_options.dart` and `android/app/google-services.json` for your own project.

### 4. Configure Supabase
- Create a free project at [supabase.com](https://supabase.com).
- Create a **public Storage bucket** (default name used in this project: `mri-reports`).
- Run the SQL policies in [`supabase_mri_reports_storage.sql`](./supabase_mri_reports_storage.sql) inside the Supabase SQL Editor.
- Update `lib/supabase_config.dart` with your own Project URL and anon key:
```dart
static const String supabaseUrl = 'YOUR_SUPABASE_URL';
static const String supabaseAnonKey = 'YOUR_SUPABASE_ANON_KEY';
static const String supabaseBucket = 'mri-reports';
```

### 5. ⚠️ AI Model Setup (required — not included in this repo)

The `.tflite` model file is **too large for a normal Git push** (GitHub blocks files over 100MB), so it is hosted separately instead of being committed to this repository.

**Steps to set it up:**
1. Download the model file from the [GitHub Releases page](https://github.com/AryanAfzal2906/teleneuro/releases).
2. Place the downloaded file at:
   `assets/vit_fyp_direct.tflite`
3. Confirm it's registered in `pubspec.yaml` (already included in this repo):
```yaml
flutter:
  assets:
    - assets/vit_fyp_direct.tflite
```
4. Run `flutter pub get` again, then rebuild the app.

> Model training and export details are documented in `final-fyp.ipynb`.

### 6. Run the app
```bash
flutter run
```

---

## 🔒 Security Notes

- Never commit real Firebase/Supabase keys to a public repository — use environment-specific config or `--dart-define` for production.
- Firestore & Storage rules should restrict read/write access appropriately before going to production (this project uses permissive `anon` policies for development — see `supabase_mri_reports_storage.sql`).

---

## 🔭 Future Work

- 3D Vision Transformer variants for full MRI volumes (NIfTI) instead of 2D slices
- Explainable AI (attention rollout / heatmaps) to show which brain regions drove a prediction
- End-to-end encryption of cloud-stored reports and chats (HIPAA/GDPR readiness)
- Longitudinal tracking of a patient's scans over time
- More diverse real-world data, especially for the `ModerateDemented` class

---

## ⚠️ Disclaimer

TeleNeuro is an academic research project. Its AI predictions are intended for research and educational purposes only and are **not** a substitute for professional medical diagnosis. Always consult a qualified neurologist.

---

## 🙏 Acknowledgements

Supervised by **Dr. Rabbia Mahum**, Department of Computer Science, UET Taxila. Thanks to the department for the academic environment and resources that made this project possible.

---

## 📜 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.
Copyright © 2026 Aryan Afzal and Malik Anas Ahmed.

---

## 👨‍💻 Authors

**Aryan Afzal** — AI & Backend Lead
🎓 UET Taxila (22-CS-89)
🔗 GitHub: [@AryanAfzal2906](https://github.com/AryanAfzal2906)
📧 Email: <afzalaryan2003@gmail.com>
💼 LinkedIn: (https://www.linkedin.com/in/aryan-afzal-316926369)

**Malik Anas Ahmed** — Mobile Application Lead
🎓 UET Taxila (22-CS-150)
📧 anasahmed.appdev@gmail.com
🔗 [LinkedIn](https://www.linkedin.com/in/malikanasahmed)

---

<p align="center">Made with ❤️ using Flutter, Firebase, Supabase & PyTorch</p>
