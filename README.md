# Hotel Booking Cancellations — Project README

## Project overview
This project analyzes the "Hotel Booking Demand" dataset (Kaggle) to predict whether a hotel booking will be canceled and to identify the factors that most strongly influence cancellations. The goal is to build an interpretable, reproducible classification pipeline and provide concise business recommendations that can help hotels reduce revenue loss.

Dataset source: https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand

---

## What I did (summary)
- Performed exploratory data analysis (EDA) to inspect distributions, missing values, and seasonality.
- Cleaned the data: filled sensible defaults for missing values, removed invalid records (e.g., bookings with zero guests), and capped extreme outliers in financial or time fields.
- Engineered features: `total_guests`, `total_nights` and encoded categorical variables using one-hot encoding.
- Trained and evaluated models: Logistic Regression (baseline) and Random Forest (final). Evaluated with accuracy, confusion matrix, precision/recall, and inspected feature importances.
- Exported the notebook and produced a PDF report for sharing with stakeholders.

---

## How it works (pipeline)
1. Load raw data (`hotel_bookings.csv`).
2. Inspect columns, data types, and missing values.
3. Clean: fill `children` with 0, fill `country` with mode, set missing `agent`/`company` to 0, drop invalid rows, cap outliers like `lead_time` and `adr`.
4. Feature engineering: create `total_guests`, `total_nights`, and select features for modeling.
5. Preprocess: one-hot encode categorical variables, scale numeric features with `StandardScaler`.
6. Split data (train/test) with stratification on target to preserve class balance.
7. Train baseline and final models, evaluate and interpret results.

---

## Dataset summary (current snapshot)
- Rows: **119,390**
- Columns: **32**
- Target (`is_canceled`) distribution: **Not canceled = 75,166 (63.0%)**, **Canceled = 44,224 (37.0%)**
- Notable missing counts:
  - `company`: 112,593 missing (many bookings have no company ID)
  - `agent`: 16,340 missing
  - `country`: 488 missing
  - `children`: 4 missing

This snapshot was taken from `hotel_bookings.csv` in this repository.

---

## Column glossary (what each column means)
Below is a concise explanation of each column in the dataset so a reader understands the raw inputs used in the analysis.

- `hotel` — Hotel type (e.g., City Hotel, Resort Hotel).
- `is_canceled` — Target: 1 = canceled, 0 = not canceled.
- `lead_time` — Number of days between booking and arrival.
- `arrival_date_year` — Year of arrival date.
- `arrival_date_month` — Month name of arrival.
- `arrival_date_week_number` — Calendar week of arrival.
- `arrival_date_day_of_month` — Day of month for arrival.
- `stays_in_weekend_nights` — Number of weekend nights (Sat/Sun) booked.
- `stays_in_week_nights` — Number of week nights (Mon–Fri) booked.
- `adults` — Number of adults in the booking.
- `children` — Number of children in the booking.
- `babies` — Number of babies in the booking.
- `meal` — Type of meal booked (e.g., BB = Bed & Breakfast).
- `country` — Country of the guest (ISO code).
- `market_segment` — Market segment designation (e.g., Online TA, Groups).
- `distribution_channel` — Channel through which the booking was made (e.g., TA/TO, Direct).
- `is_repeated_guest` — 1 if the customer is a repeated guest, else 0.
- `previous_cancellations` — Number of previous bookings canceled by the customer.
- `previous_bookings_not_canceled` — Number of previous bookings not canceled by the customer.
- `reserved_room_type` — Code of room reserved.
- `assigned_room_type` — Code of room assigned.
- `booking_changes` — Number of changes made to the booking.
- `deposit_type` — Type of deposit (No Deposit, Non Refund, Refundable).
- `agent` — ID of travel agency that made the booking (or 0 if none).
- `company` — ID of the company that made the booking (or 0 if none).
- `days_in_waiting_list` — Number of days the booking was on the waiting list.
- `customer_type` — Type of customer (Transient, Contract, Group etc.).
- `adr` — Average Daily Rate (average price per day for the booking).
- `required_car_parking_spaces` — Number of parking spaces required.
- `total_of_special_requests` — Number of special requests made by the customer (e.g., late check-in).
- `reservation_status` — Reservation status at dataset export (e.g., Canceled, Check-Out, No-Show).
- `reservation_status_date` — Date of the last reservation status change.

---

## What I used (tools & libraries)
- Python 3.11
- Jupyter Notebook / `.ipynb`
- pandas, numpy for data manipulation
- matplotlib, seaborn for visualization
- scikit-learn for modeling and evaluation
- nbconvert + selenium/webdriver-manager (for HTML→PDF export fallback)

---

## Results (short)
- Random Forest outperformed Logistic Regression on this dataset in terms of balanced performance and interpretability via feature importances.
- Top predictive features: **lead_time**, **deposit_type**, **total_of_special_requests**, and selected encoded categorical variables.

---

## How to reproduce
1. Place `hotel_bookings.csv` in the project folder.
2. Install dependencies (example):
   - `pip install pandas numpy matplotlib seaborn scikit-learn nbconvert selenium webdriver-manager`
3. Run `analysis and cleaning.ipynb`; outputs include plots, model metrics, and a generated PDF report (`analysis_and_cleaning_printed.pdf`).

---


