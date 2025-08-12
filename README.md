# AlphaVue a Portfolio-Recommendation-System


[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://python.org)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.0+-red.svg)](https://streamlit.io)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![MySQL](https://img.shields.io/badge/MySQL-8.0+-orange.svg)](https://mysql.com)

> Democratizing financial advisory services through AI-powered personalized investment recommendations


## 🎯 Overview

AlphaVue is an intelligent financial advisory platform that leverages machine learning to provide personalized, data-driven investment recommendations. The system helps users understand their risk tolerance, receive suitable asset allocation strategies, and identify potentially high-performing stocks and mutual funds.

### Key Features

- 🧠 **AI-Driven Risk Profiling** - Machine learning models assess user risk tolerance
- 📊 **Modern Portfolio Theory Integration** - Optimal asset allocation using Sharpe ratio maximization  
- 🔮 **Prophet Forecasting** - Time-series analysis for stock and mutual fund predictions
- 👥 **User Clustering** - Personalized recommendations based on investor personas
- 📈 **Power BI Dashboard Integration** - Interactive analytics dashboard embedded in Streamlit
- 🌐 **Real-time Data Integration** - Live market data via Yahoo Finance API
- 🔐 **Secure Authentication** - MySQL database with bcrypt password hashing
- 📱 **Interactive Web Interface** - Clean, user-friendly Streamlit application

## 🏗️ Architecture

### System Design
```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│  Yahoo Finance  │───►│  Data Collection │───►│   ETL Pipeline  │
│      API        │    │    & Storage     │    │                 │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                                                        │
                                                        ▼
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Power BI      │◄───│  Trained Models  │◄───│  Model Training │
│   Dashboard     │    │   & Artifacts    │    │   & Validation  │
└─────────────────┘    └──────────────────┘    └─────────────────┘
        │                       │
        ▼                       ▼
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Streamlit     │◄───│  Model Loading   │    │  MySQL Database │
│  Web Interface  │    │   & Inference    │───►│ (User & Portfolio│
│  (with embedded │    │                  │    │     Storage)    │
│  Power BI)      │    └──────────────────┘    └─────────────────┘
└─────────────────┘
```

### Workflow Pipeline

#### Data Collection & Processing Pipeline
1. **Real-time Data Ingestion** - Yahoo Finance API for live market data
2. **Data Validation** - Quality checks and missing data handling
3. **Feature Engineering** - Technical indicators and derived metrics
4. **Model Training** - Train Random Forest and K-Means clustering models
5. **Forecasting** - Run Prophet models on historical price data
6. **Dashboard Creation** - Power BI analytics and visualization development
7. **Artifact Persistence** - Save trained models and processed data

#### Online Application Flow
1. **User Authentication** - Secure login/signup system
2. **Risk Assessment** - Interactive questionnaire for risk profiling
3. **Asset Allocation** - AI-recommended portfolio distribution
4. **Stock Selection** - MPT-optimized stock recommendations
5. **Mutual Fund Selection** - Performance-based fund recommendations
6. **Analytics Dashboard** - Embedded Power BI visualizations
7. **Portfolio Summary** - Comprehensive investment plan with projections

## 🛠️ Tech Stack

### Core Libraries
- **Machine Learning**: Pandas, NumPy, Scikit-learn, Prophet
- **Data Collection**: yfinance (Yahoo Finance API)
- **Optimization**: SciPy
- **Persistence**: joblib
- **Security**: bcrypt, email_validator

### Web Application & Analytics
- **Framework**: Streamlit
- **Database**: MySQL
- **Business Intelligence**: Power BI (embedded dashboards)
- **Visualization**: Plotly, Power BI integration

### Data Processing
- **API Integration**: Yahoo Finance real-time data
- **ETL Pipeline**: Custom Python scripts
- **Data Format**: API JSON → Pandas DataFrame → CSV
- **Storage**: Local file system + MySQL + Power BI datasets

## 🚀 Getting Started

### Prerequisites
```bash
Python 3.8+
MySQL Server 8.0+
Power BI Desktop (for dashboard development)
Git
```

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/alphavue.git
   cd alphavue
   ```

2. **Create virtual environment**
   ```bash
   python -m venv alphavue_env
   source alphavue_env/bin/activate  # On Windows: alphavue_env\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Database Setup**
   ```sql
   CREATE DATABASE alphavue;
   -- Run the provided schema.sql file
   mysql -u root -p alphavue < database/schema.sql
   ```

5. **Configuration**
   ```bash
   cp config/config.example.py config/config.py
   # Edit config.py with your database credentials
   ```

### Running the Application

1. **Train Models (First Time Setup)**
   ```bash
   python scripts/train_models.py
   python scripts/process_data.py
   ```

2. **Launch the Web Application**
   ```bash
   streamlit run app.py
   ```

3. **Access the Application**
   Open your browser to `http://localhost:8501`

## 📊 Data Processing & ETL Pipeline

### Data Collection Strategy

#### Real-time Market Data
- **Source**: Yahoo Finance API via yfinance library
- **Data Types**: Stock prices, mutual fund NAVs, market indices
- **Frequency**: Daily close prices, real-time quotes
- **Coverage**: Major stock exchanges, comprehensive mutual fund database

### ETL Pipeline

#### Extract
- **Yahoo Finance API**: Live stock prices and historical data
- **Market Indices**: Benchmark data for performance comparison
- **Mutual Fund NAVs**: Historical and current fund performance
- **Synthetic User Data**: Generated profiles for model training

#### Transform
- **Data Standardization**: Consistent date formats and price normalization
- **One-Hot Encoding** for categorical features (investment goals, risk preferences)
- **StandardScaler** for numerical feature normalization (age, investment horizon)
- **Technical Indicators** calculation:
  - Simple Moving Average (SMA)
  - Relative Strength Index (RSI) 
  - Bollinger Bands
  - MACD indicators
- **Forward-fill imputation** for missing time-series values
- **CAGR Calculation**: Compound Annual Growth Rate for performance metrics

#### Load
- **Structured Storage**: Processed data stored in MySQL database
- **Power BI Datasets**: Optimized data models for dashboard consumption
- **CSV Exports**: Aggregated datasets for model training
- **Model Artifacts**: Serialized models using joblib

### Data Quality & Validation

#### Data Sanity Checks
- **API Response Validation**: Verify data completeness and format
- **Date Range Consistency**: Ensure continuous time-series data
- **Price Anomaly Detection**: Statistical outlier identification
- **Missing Data Handling**: Forward-fill with validation limits
- **Prophet R² Threshold**: Minimum 0.75 for forecast reliability
- **Data Availability Checks**: Minimum historical data requirements
- **Schema Validation**: Consistent data structure alignment

#### Data Cleaning Process
- **Duplicate Removal**: Handle redundant API responses
- **Outlier Treatment**: Statistical methods for extreme value handling
- **Data Type Consistency**: Ensure proper numeric and date formats
- **Null Value Strategy**: Context-aware imputation methods

### Data Transformation Techniques

#### Feature Engineering
- **Price Momentum**: Rolling returns and volatility calculations
- **Market Correlation**: Asset relationship analysis
- **Seasonality Features**: Monthly/quarterly performance patterns
- **Risk Metrics**: Beta calculation, correlation with market indices

#### Imputation Strategies
- **Time-series Data**: Forward-fill method for price continuity
- **User Profile Data**: Mean/mode imputation for demographic features
- **Market Data**: Interpolation for missing trading day values
- **Validation**: Cross-validation to ensure imputation quality

### Model Training & Validation

#### 1. Risk Profiling Model
- **Algorithm**: Random Forest Classifier
- **Purpose**: Predict user risk tolerance (Low/Medium/High)
- **Features**: Age, investment horizon, financial goals, market reaction preferences
- **Training Data**: Synthetic user profiles (5000+ samples)
- **Validation**: Stratified K-fold cross-validation
- **Evaluation Metrics**: 
  - Accuracy score (target: >85%)
  - Precision, recall, F1-score per risk class
  - Confusion matrix analysis
  - ROC-AUC score

#### 2. User Clustering Model  
- **Algorithm**: K-Means Clustering
- **Purpose**: Group users into investor personas for personalized recommendations
- **Features**: Scaled demographic and preference data
- **Optimization**: Elbow method for optimal cluster determination
- **Validation**: Silhouette score analysis
- **Evaluation Metrics**:
  - Within-cluster sum of squares (WCSS)
  - Silhouette coefficient
  - Cluster stability analysis

#### 3. Time-Series Forecasting
- **Algorithm**: Prophet (Meta's forecasting library)
- **Purpose**: Predict stock and mutual fund future performance
- **Features**: Historical prices, volume, seasonal patterns
- **Validation**: Walk-forward validation, R² score threshold (≥0.75)
- **Evaluation Metrics**:
  - Mean Absolute Percentage Error (MAPE)
  - Root Mean Square Error (RMSE)
  - R² coefficient of determination
  - Directional accuracy (up/down prediction)

#### 4. Portfolio Optimization
- **Method**: Modern Portfolio Theory (MPT)
- **Objective**: Maximize Sharpe ratio for optimal risk-adjusted returns
- **Constraints**: User-defined risk tolerance and asset allocation limits
- **Optimization**: Sequential Least Squares Programming (SLSQP)
- **Evaluation Metrics**:
  - Sharpe ratio maximization
  - Portfolio volatility vs. expected return
  - Maximum drawdown analysis
  - Correlation matrix analysis

### Model Selection Criteria

#### Performance Benchmarks
- **Risk Classifier**: >85% accuracy with balanced precision/recall
- **Forecasting Models**: R² > 0.75 for reliable predictions
- **Clustering Quality**: Silhouette score > 0.5
- **Portfolio Optimization**: Sharpe ratio > market benchmark

#### Model Comparison Framework
- **Cross-validation**: Time-series aware validation techniques
- **Baseline Comparison**: Simple heuristic models as benchmarks
- **Statistical Significance**: Hypothesis testing for model superiority
- **Business Impact**: Actual vs. predicted portfolio performance

## 💾 Data Storage Architecture

### Database Schema Design

#### Core Tables
```sql
-- User authentication and profile
users: id, username, email, password_hash, created_at, last_login

-- Risk assessment and portfolio configuration  
portfolios: id, user_id, risk_profile, allocation_equity, allocation_debt, 
           allocation_gold, total_investment, created_at, updated_at

-- Stock recommendations with performance metrics
portfolio_stocks: id, portfolio_id, symbol, company_name, allocation_percentage, 
                 expected_return, predicted_price, confidence_score

-- Mutual fund recommendations  
portfolio_mutual_funds: id, portfolio_id, fund_name, fund_code, allocation_percentage, 
                       historical_cagr, expense_ratio, fund_category

-- Market data cache for performance optimization
market_data: id, symbol, date, open_price, high_price, low_price, close_price, 
            volume, adjusted_close, created_at

-- User activity tracking
user_sessions: id, user_id, login_time, logout_time, ip_address, user_agent
```

#### Data Storage Strategy
- **Relational Data**: MySQL for transactional data and user information
- **Time-series Data**: Optimized tables with date indexing for market data
- **Model Artifacts**: File system storage using joblib serialization
- **Power BI Datasets**: Direct database connections and CSV exports
- **Cache Layer**: Redis for frequently accessed market data (future enhancement)

### Data Persistence & Backup
- **Automated Backups**: Daily MySQL database backups
- **Model Versioning**: Git-based model artifact versioning
- **Data Retention**: 5-year historical data retention policy
- **Disaster Recovery**: Cloud backup strategy with point-in-time recovery

## 📈 Performance Metrics

### Model Evaluation
- **Risk Classifier Accuracy**: Target >85%
- **Forecast Reliability**: R² score >0.75
- **Portfolio Optimization**: Sharpe ratio maximization
- **Data Coverage**: Complete time-series for analysis

### System Performance
- **Response Time**: <3 seconds for recommendations
- **Data Processing**: Efficient ETL pipeline
- **Model Loading**: Optimized artifact loading
- **Database Queries**: Indexed for fast retrieval

- #### Dashboard Components
- **Portfolio Performance Overview**: Real-time portfolio value and returns
- **Asset Allocation Visualization**: Interactive pie charts and treemaps
- **Market Trends Analysis**: Historical price movements and technical indicators
- **Risk Metrics Dashboard**: Volatility, Sharpe ratio, and drawdown analysis
- **Comparative Analysis**: Benchmark comparisons and peer performance

#### Key Performance Indicators (KPIs)
- **Portfolio Metrics**: Total value, daily P&L, YTD returns
- **Risk Indicators**: Beta, standard deviation, maximum drawdown
- **Performance Ratios**: Sharpe ratio, Sortino ratio, alpha generation
- **Asset Breakdown**: Sector allocation, geographic distribution

#### Interactive Features
- **Date Range Filtering**: Custom time period analysis
- **Asset Drilling**: Click-through from portfolio to individual holdings
- **Comparative Views**: Multiple portfolio comparison capabilities
- **Real-time Updates**: Live data refresh from Yahoo Finance API

### Streamlit Integration
- **Embedded Power BI**: Seamless dashboard integration within web app
- **Responsive Design**: Dashboard adapts to different screen sizes
- **User Context**: Personalized views based on user portfolio
- **Export Capabilities**: PDF reports and data export functionality

### Visualization Strategy
- **Data Storytelling**: Clear narrative flow from risk assessment to recommendations
- **Progressive Disclosure**: Layered information presentation
- **Interactive Elements**: Hover effects, drill-down capabilities, filtering
- **Mobile Optimization**: Touch-friendly interface for mobile users# AlphaVue: AI-Powered Financial Advisor 📈


## 🔮 Future Enhancements

### Planned Technical Features
- **Advanced ML Models** - LSTM neural networks for enhanced time-series forecasting
- **Real-time Streaming** - Apache Kafka for live market data processing  
- **Sentiment Integration** - NLP analysis of financial news and social media
- **Options Analytics** - Greeks calculation and options strategy recommendations
- **ESG Integration** - Environmental, Social, Governance scoring in recommendations
- **Crypto Portfolio** - Cryptocurrency analysis and portfolio inclusion

### Platform Enhancements  
- **Mobile Applications** - Native iOS/Android apps with offline capabilities
- **API Development** - RESTful APIs for third-party integrations
- **Advanced Analytics** - Monte Carlo simulations for risk scenario analysis
- **Social Features** - Portfolio sharing and community investment insights
- **Robo-advisor** - Automated rebalancing and tax-loss harvesting
- **Multi-currency** - International market support and currency hedging

### Power BI Dashboard Expansions
- **Predictive Analytics** - Forward-looking performance projections
- **Stress Testing** - Portfolio performance under various market conditions
- **Sector Analysis** - Deep-dive industry and sector performance analytics
- **Global Markets** - International market correlation and opportunity analysis
- **Alternative Investments** - REITs, commodities, and alternative asset analysis

### Infrastructure & Scalability
- **Cloud Migration** - AWS/Azure deployment with auto-scaling
- **Microservices** - Service-oriented architecture for better scalability
- **Data Pipeline** - Apache Airflow for automated ETL orchestration
- **Performance Optimization** - Redis caching and database optimization
- **Security Enhancement** - OAuth integration, two-factor authentication
- **Compliance** - GDPR, SOX compliance for financial data handling


## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Authors

- **Yash Bodake** - *Initial work* - [YourGitHub](https://github.com/yashbodake)

## 🙏 Acknowledgments

- **Prophet** by Meta for time-series forecasting capabilities
- **Streamlit** for the intuitive web application framework
- **Scikit-learn** for robust machine learning algorithms
- **Modern Portfolio Theory** by Harry Markowitz for optimization principles

## 📞 Support

For support and questions:
- 📧 Email: yashbodake4444@gmail.com
- 

---

⭐ **Star this repository if you found it helpful!**

Made with ❤️ for democratizing financial advisory services
