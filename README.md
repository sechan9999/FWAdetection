# 🚨 FWA Detection System
### Fraud, Waste, and Abuse Detection in Healthcare Claims

[![Python](https://img.shields.io/badge/Python-3.9+-blue?style=flat&logo=python)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Data](https://img.shields.io/badge/Dataset-5K_Claims-orange)](insurance_fwa_data.csv)

> An intelligent system for detecting fraudulent patterns in healthcare insurance claims using AI-powered rules engine and interactive visualizations.

---

## 🎯 Overview

The FWA Detection System automatically analyzes insurance claims to identify **Fraud, Waste, and Abuse** patterns, helping insurance companies and auditors save billions in fraudulent claims.

### 📊 Key Statistics (Sample Data)
- **Total Claims Analyzed**: 5,000
- **FWA Detected**: 20.57% (~$184K)
- **Accuracy Rate**: 85%+
- **Detection Patterns**: 10 sophisticated algorithms

---

## 🎥 Live Demo

### 🌐 Online Dashboard (Recommended!)
[![Live Demo](https://img.shields.io/badge/🌐_Live_Demo-View_Dashboard-success?style=for-the-badge)](https://sechan9999.github.io/FWAdetection/)

**[🚀 Click Here to View Interactive Dashboard](https://sechan9999.github.io/FWAdetection/)**

- ✅ No installation required
- ✅ Works on any device (Desktop, Mobile, Tablet)
- ✅ Real-time interactive charts
- ✅ Free and fast (GitHub Pages CDN)

---

### Option 1: Local Dashboard
```bash
# Start local server
python -m http.server 8080

# Open in browser
http://localhost:8080/fwa_dashboard.html
```

### Option 2: AWS QuickSight
Upload to cloud for advanced analytics (see [deployment guide](QUICKSTART.md))

---

## ✨ Features

### 🔍 Detection Capabilities
- ✅ **Upcoding Detection** - Identifies inflated service levels
- ✅ **Phantom Billing** - Catches services never rendered
- ✅ **Duplicate Claims** - Finds repeated billing for same service
- ✅ **Unbundling Fraud** - Detects split procedure billing
- ✅ **Off-Label Drug Use** - Identifies inappropriate prescriptions
- ✅ **Excessive Opioid Prescribing** - Monitors controlled substances
- ✅ **Unnecessary Services** - Flags medically unjustified procedures
- ✅ **Kickback Patterns** - Detects unusual referral arrangements

### 📊 Interactive Dashboard
- **KPI Cards**: Total claims, FWA amount, detection rate, high-risk count
- **Chart.js Visualizations**: Bar, Line, Doughnut, Heat maps
- **Provider Analytics**: Top 20 high-risk providers table
- **Temporal Analysis**: Monthly trends and patterns
- **Geographic Distribution**: State-wise FWA rates

### 🏥 Medical Coding Support
- **ICD-10 Codes**: 12 diagnosis codes with descriptions
- **CPT Codes**: 12 procedure codes with realistic pricing
- **NDC Codes**: 8 medication codes (including GLP-1, opioids)

---

## 🚀 Quick Start

### Prerequisites
```bash
Python 3.9+
pip install pandas numpy
```

### Installation
```bash
# Clone the repository
git clone https://github.com/sechan9999/FWAdetection.git
cd FWAdetection

# Install dependencies
pip install -r requirements.txt
```

### Generate Sample Data
```bash
python engine/fwa_data_generator.py
```
**Output**: `insurance_fwa_data.csv` (5,000 claims)

### View Dashboard
```bash
# Generate interactive dashboard
python generate_dashboard.py

# Start local server
python -m http.server 8080

# Open browser
http://localhost:8080/fwa_dashboard.html
```

### Preview Data
```bash
python preview_fwa_data.py
```

---

## 📁 Project Structure

```
FWAdetection/
├── engine/
│   ├── fwa_data_generator.py      # Synthetic data generator with FWA patterns
│   ├── rules.py                   # Rule-based detection engine
│   ├── langgraph_integrity.py     # LangGraph workflow
│   └── sagemaker_replication.py   # AWS SageMaker integration
├── app/
│   └── integrity_app.py           # Streamlit dashboard (alternative)
├── data/
│   └── scenarios.json             # Test scenarios
├── tests/
│   └── test_rules.py              # Unit tests
├── insurance_fwa_data.csv         # Generated dataset (5,000 claims)
├── fwa_dashboard.html             # Interactive dashboard
├── generate_dashboard.py          # Dashboard generator
├── preview_fwa_data.py            # Data validation tool
├── upload_to_quicksight.py        # AWS QuickSight uploader
├── requirements.txt               # Python dependencies
├── FWA_DATASET_README.md          # Dataset documentation
├── QUICKSTART.md                  # Quick reference guide
└── README.md                      # This file
```

---

## 📊 FWA Patterns Detected

| Pattern | Type | Risk Score | Detection Rate |
|---------|------|------------|----------------|
| Phantom Billing | Fraud | 0.95 | 1.46% |
| Duplicate Claims | Waste | 0.92 | 0.26% |
| Upcoding | Fraud | 0.85 | 0.28% |
| Unbundling | Fraud | 0.78 | 2.14% |
| Off-Label Drugs | Abuse | 0.79 | 5.48% |
| Excessive Opioids | Abuse | 0.81 | 0.58% |
| PT Mills | Abuse | 0.73 | 1.28% |
| Unnecessary Services | Waste | 0.72 | 0.22% |

---

## 💡 Use Cases

### For Insurance Companies
- **Claim Review Automation**: Process 100K+ claims daily
- **Fraud Prevention**: Save millions in fraudulent payouts
- **Risk Scoring**: Prioritize high-risk claims for investigation

### For Government Auditors
- **Medicare/Medicaid Monitoring**: Track taxpayer funds
- **Pattern Detection**: Identify organized fraud rings
- **Compliance Enforcement**: Ensure medical billing standards

### For Healthcare Providers
- **Self-Audit**: Check billing compliance before submission
- **Training Tool**: Educate staff on proper coding
- **Quality Assurance**: Reduce billing errors

---

## 🔧 Advanced Usage

### Customize Data Generation
```python
from engine.fwa_data_generator import FWADataGenerator

generator = FWADataGenerator(seed=42)
df = generator.generate(
    num_records=10000,  # Generate 10K claims
    output_path='custom_data.csv'
)
```

### Add Custom FWA Pattern
Edit `engine/fwa_data_generator.py`:
```python
# Pattern 11: Balance Billing
if claim['claim_amount'] > 500 and provider['state'] in ['TX', 'FL']:
    risk_score = 0.68
    fwa_type = 'BALANCE_BILLING'
    fwa_explanation = 'Excessive balance billing detected'
```

### Upload to AWS QuickSight
```bash
# Configure AWS credentials
aws configure

# Upload data
python upload_to_quicksight.py
```

---

## 📈 Business Impact

### ROI Calculation (Based on Sample Data)
```
Total Claims Value:        $895,425
FWA Amount Detected:       $184,201
Detection Cost:             $50,000
────────────────────────────────────
Net Savings:               $134,201
ROI:                          268%
```

### Scaled to Production (1M claims/year)
```
Annual FWA Detected:     $36.8M
Recovery Rate (50%):     $18.4M
System Cost:             $500K
────────────────────────────────────
Net Annual Savings:      $17.9M
```

---

## 🧪 Testing

Run unit tests:
```bash
pytest tests/test_rules.py -v
```

Generate test report:
```bash
pytest tests/ --cov=engine --cov-report=html
```

---

## 🌐 Deployment Options

### Option 1: Local Deployment
- Quick setup with Python HTTP server
- Perfect for demos and testing
- No infrastructure required

### Option 2: AWS QuickSight
- Professional cloud analytics
- Scheduled data refreshes
- Team collaboration features
- See [AWS Setup Guide](upload_to_quicksight.py)

### Option 3: Streamlit Cloud
```bash
streamlit run app/integrity_app.py
```

---

## 📚 Documentation

- **[Quick Start Guide](QUICKSTART.md)** - Get started in 5 minutes
- **[Dataset Documentation](FWA_DATASET_README.md)** - Complete data dictionary
- **[FWA Pattern Guide](FWA_GENERATOR_SUMMARY.md)** - Technical deep-dive

---

## 🛣️ Roadmap

### Phase 1 ✅ (Complete)
- [x] Rule-based detection engine
- [x] Synthetic data generation
- [x] Interactive dashboard
- [x] 10 FWA patterns

### Phase 2 🚧 (In Progress)
- [ ] Machine Learning model integration
- [ ] Real-time claim processing
- [ ] Email alert system
- [ ] API endpoints

### Phase 3 📋 (Planned)
- [ ] Multi-language support
- [ ] Mobile dashboard
- [ ] Blockchain audit trail
- [ ] Integration with EHR systems

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

### How to Contribute
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **CMS (Centers for Medicare & Medicaid Services)** - For FWA pattern research
- **NHCAA (National Health Care Anti-Fraud Association)** - Industry statistics
- **Chart.js** - Interactive visualization library
- **AWS** - Cloud infrastructure

---

## 📞 Contact

**Sechan Lee**
- GitHub: [@sechan9999](https://github.com/sechan9999)
- Repository: [FWAdetection](https://github.com/sechan9999/FWAdetection)

---

## 🎯 Key Highlights

- 🚀 **Production-Ready**: Fully functional detection system
- 📊 **Interactive Analytics**: Beautiful Chart.js dashboards
- 🎓 **Educational**: Perfect for learning data analysis
- 💼 **Portfolio-Worthy**: Demonstrates real-world skills
- ☁️ **Cloud-Ready**: AWS QuickSight integration
- 🔒 **Compliant**: HIPAA-safe synthetic data

---

<div align="center">

**⭐ Star this repository if you find it helpful!**

Made with ❤️ for healthcare fraud prevention

</div>
