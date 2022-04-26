# Recurrent Data Scientist Take-Home Exercise

At Recurrent, we work with data we collect from or about electric vehicles
(EVs). Using Python in a Jupyter notebook, we’d like you to begin setting 
up a prototype for a model that will predict the estimated range
(at full charge) for any vehicle like those in our training data. We’re not 
providing sufficient data to actually train such a model but would like to 
see how you approach the problem, what tools you decide to use, etc. 

We’ll use this notebook as a launching point for discussion in our next interview. 

### The assignment
In a Jupyter notebook:

1. Read in the sample data (described below); parse fields as appropriate for your 
   downstream use case(s), and explore the data.
2. The age of a vehicle’s battery is often an important feature to consider when 
   predicting its range. Use the information provided to derive an estimate for the 
   battery age of each observation that you can use later as a feature in your model.
3. Do whatever preprocessing is necessary for the modeling approach you choose for 
   the next step.
4. Outline the steps to predict the range at full charge (the equivalent of 
   `charge_reading = 1`) for any new vehicle. Choose a modeling algorithm to use and 
   begin setting up the model training and evaluation code. It will be important to
   quantify the uncertainty of the model predictions when this model is put into production,
   so please consider (but you don’t need to implement) approaches to doing that within
   your chosen framework.
    - You can choose the features that you suspect will make the most sense to train with, 
      just be prepared to discuss why you included or didn’t include different things.
    - Outline the steps you’d take to tune, train, and evaluate the model(s). 
    - Pseudocode is acceptable after you’ve created the dataset you’ll train with. We would like to
      see you import the libraries or functions you’ll use during tuning and training even
      if you just reference them in pseudocode.

Think about this as a notebook that you might throw together during a design spike, then 
share with the rest of the data science team (asynchronously) so they could follow your 
thinking and provide feedback.

### What we expect
- We **don't** expect you to spend more than about 2 hours working on this. Your time is valuable, 
  please don't spend any longer
  on it, even if you didn't finish it! One of our goals with this assignment is to set the 
  foundation for a productive conversation in the next interview - we can talk through how you
  would approach the unfinished pieces at that time.
- At junctures where you make assumptions, consider multiple paths forward, or you encounter 
  likely edge cases, please add commentary in the form of markdown cells or in-line comments
  in your code. We'd rather see more of your thought process than less.
- We’re not looking for a polished presentation-ready notebook - what we’re hoping to simulate
  with this assignment is the first steps you might take to explore the data and prototype 
  some code, before getting a rough model up and running.  With that in mind, please leave 
  in cells that show your exploration or thought processes so that we can follow your work. 
- At the end of the notebook, include a markdown cell with a discussion of what you would do 
  differently or improve if you had more time/more data/additional data sources/etc.
- Please try to make it easy for us to run the cells in your notebook (those that aren't 
  pseudocode) by using relatively up-to-date versions of Python and the packages
  you import.
- There is no deadline for this, just send it to us when you are ready.
- Submit your Jupyter notebook by emailing it to us (you can email the `.ipynb` file itself,
  or a link to the file hosted on a cloud service). Please don't include your name or other
  identifying info in your notebook - we will pass your notebook to team members to review
  blind (without knowing applicant identities).

### The sample data
We've provided four files with small sets of sample data to use in this assignment. 
This is made up data, but we tried to make it representative of realistic datasets and 
simplified schemas.

### `ev_data.csv`
This file contains observations that show information on range and charge level
for individual vehicles.
- `vehicle_id`: A unique identifier tied to the vehicle, expressed as a
  string.
- `vehicle_model_id`: An integer key used to look up information about the vehicle 
  in the `vehicle_models` CSV.
- `charge_reading`: The vehicle’s State of Charge (SoC), a decimal number
  representing the current charge level of the battery in terms of percentage
  (for example, 0.33 means the battery is 33% charged).
- `range_estimate`: The estimated range that the vehicle can drive before the
  battery is depleted, expressed in miles as a decimal number. This is the number
  that a driver sees on their dashboard at the time the observation was recorded.
- `odometer`: The vehicle’s current odometer reading, expressed in miles as an
  integer.
- `plugged_in`: Whether or not the vehicle is plugged in at the time of the
  reading, expressed as a boolean.
- `charging_state`: Whether or not the vehicle is actively charging at the time of
  the reading, expressed as a string.
- `created_at`: Timestamp of the reading, expressed in a string of the format
  "yyyy-mm-dd hh:mm:ss ZZZZ", the timezone is UTC for all readings.
- `zipcode`: The zipcode where the vehicle was at the time of the observation,
   expressed as a string.

### `manufacture_dates.csv`
This file provides the vehicle manufacture date for each car.
- `vehicle_id`: A unique identifier tied to the vehicle, expressed as a
  string.
- `manufacture_date`: The date of manufacture for the vehicle, expressed as a string 
  of the format `yyyy-mm-dd`.

### `vehicle_models.csv`
This file contains information about the vehicles like make, model, model year,
battery capacity, etc.
- `vehicle_model_id`: An unique identifier tied to the vehicle model, expressed as an integer.
- `make`: The name of the company that makes the vehicle, expressed a string.
- `model`: The model of the vehicle, expressed as a string.
- `trim`: The trim level of the vehicle, expressed as a string. For some makes and models 
  different trims have different battery configurations, while for others they are purely 
  about cosmetic features.
- `model_year`: The model year of the vehicle, expressed as an integer. This is often 
  different from the year the car was actually manufactured.
- `type`: Whether the car is a BEV (battery electric vehicle) or PHEV 
  (plug-in hybrid electric vehicle), expressed as a string.
- `epa_rated_miles`: This is an approximation of how many miles this kind of car can drive 
  on its electric charge when it is new under controlled conditions. It is based on some 
  standardized testing methodologies,
  but there is a lot of flexibility in how different automakers perform the tests and combine
  the resulting numbers. Expressed as a float.
- `battery_kwh`: The nominal amount of energy in this vehicle's battery when new, measured in
  kWh. Expressed as a float.

### `weather_history.csv`
- `zipcode`: The zipcode where the vehicle was at the time of the observation,
   expressed as a string.
- `climate_descriptor_1`: a placeholder for a quantitative measure of the historical 
  exposure to high temperatures in this location, expressed as an integer.
- `climate_descriptor_2`: another placeholder for a quantitative measure of the historical 
  exposure to very low temperatures in this location, expressed as an integer.
