# hair-app
Monitoring tool to help me book hair appointments at Great Clips

The basic idea is to create 2 apps:

### A UI App
Resonsibilities:
- accept a state or city and state (USA)
- present a dashboard to the user about all Great Clips stores in that region. The dashboard will show, for each store:
  - Current `wait-time`
  - Best window of time (from now til close-time) where they wait is going to be less than 15 minutes
  - A time-series graph that shows UCL and LCL boundaries and the actual and average `wait-time`
- Respond with `Data Not Aavailable` when the system does not track info for a given state or city & state combination. In these cases
  - Offer option to user to start tracking information for that state or city & state combination

### A series of back-end services: REST API, MQTT Broker, Canary Labs Historian, etc.
Responsibilities:
- Expose an API surface that provides all features needed by the `UI App`
- Use an MQTT Broker to store current state data and calculations
- Use a format, a Unified Namespace or `UNS`, similar to `ISA-95` to classify data:
  - Great-Clips
    - State
      - City
        - Store-Address
  - An MQTT Broker topic to capture/store data and information about a store in New Prague, MN would be:
    - /great-clips/mn/new-prague/100-main-street
    - /great-clips/{state}/{city}/{top-address-line}

