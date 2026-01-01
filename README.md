## 1. The Basic Science: Why do we need to "Predict"?

To understand the project, we first need to understand how satellites move.

### What is a TLE (Two-Line Element)?

Satellites don't have GPS like our phones. Instead, we use a **TLE**. It’s a standardized data format (literally two lines of text) that contains the "DNA" of a satellite's orbit: its speed, its tilt, and its height. However, TLEs get outdated quickly because of atmospheric drag and the Earth's gravity, so we constantly need to fetch updated ones from databases like **CelesTrak**.

### The Geometry of Visibility

Imagine you are standing in the middle of the IIT Madras campus. The sky is like a giant dome over you.

* **Altitude:** How high the satellite is above your horizon (0° is the horizon, 90° is directly overhead).
* **Azimuth:** The compass direction (North, East, South, West).
* **The Window:** A satellite is only "visible" for communication when its altitude is above a certain degree (usually >10°). Because satellites move at thousands of miles per hour, this "window" usually only lasts 5 to 15 minutes.

---

## 2. The Logic: How the Code Works

The project follows a pipeline from raw orbital data to a smart prediction model.

### Step A: Data Generation (The Simulator)

Since we can't wait months to collect real-time data, we use a library called `skyfield`.

1. We give it the coordinates of **IIT Madras** ().
2. We feed it TLEs for satellites like the **International Space Station (ISS)**.
3. The code "simulates" the next 90 days, calculating the satellite's position every minute. If the satellite is above the horizon, the code records the time and duration.

### Step B: The Feature Engineering

To help the AI learn, we give it specific "clues" (Features):

* **Altitude & Azimuth:** Where is it right now?
* **Distance:** How far away is it?
* **Time Factors:** Hour of the day and day of the year (useful for seasonal variations).

---

## 3. The AI Brain: Choosing the Best Model

The team tested four different types of "brains" to see which one predicted the pass duration most accurately.

| Model | How it works | Result |
| --- | --- | --- |
| **Linear Regression** | Draws a straight line through data. | Basic, low accuracy. |
| **Random Forest** | Uses a "forest" of decision trees to vote on the answer. | **Very Strong Performance.** |
| **Gradient Boosting** | Learns from its mistakes in rounds. | Excellent accuracy. |
| **Deep Learning (Neural Network)** | Mimics the human brain with layers of "neurons." | **Most Advanced**; handles complex patterns well. |

---

## 4. Visualizing the Results

The project includes several high-level visualizations to make the data understandable:

* **Polar Sky Map:** This looks like a circular radar screen. It shows the "arc" of the satellite as it travels across the sky over IIT Madras.
* **Training History:** A graph showing how the Deep Learning model's "error" decreased as it studied the data more.
* **Actual vs. Predicted Plot:** A scatter plot where a perfect prediction sits on a red diagonal line. Our model stays very close to this line, meaning it is highly reliable.

---

## 5. Why does this matter?

If you are running a ground station at IIT Madras, you need to know exactly when to point your antennas at the sky to download data or send commands.

* **Efficiency:** You don't waste energy searching the sky.
* **Scheduling:** If multiple satellites are passing at once, the AI helps you prioritize the one with the longest visibility window.

---

## 6. Practical Use: Why IIT Madras Needs This
* **Antenna Scheduling:** The IITM ground station can use this AI to decide which satellite to track first if two appear at once.
* **Energy Savings:** The motors that move satellite dishes consume power. By knowing the duration in advance, the system can stay in "sleep mode" until the exact second the window opens.

### Summary of Tech Stack

* **Physics:** `skyfield` (Orbital mechanics).
* **Data Science:** `pandas`, `numpy`.
* **Machine Learning:** `scikit-learn`, `XGBoost`.
* **Deep Learning:** `TensorFlow/Keras`.

---

**Would you like me to explain how to interpret the TLE data format specifically, or dive deeper into how the Random Forest model makes its decisions?**
