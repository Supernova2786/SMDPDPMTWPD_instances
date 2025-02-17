The data needed for this research can be categorized into two classes: vehicle data and order data. Vehicle data consists of the number of vehicles for which freight is searched and per vehicle the name (for identification), the capacity (the space left and for which freight needs to be found in LDMs), the current weight, the maximum allowed weight, the start location (country and zip code) the time at which the vehicle becomes empty (start date and time), one or multiple end location(s) (country and zip code(s)) and time at which the vehicle should be at one of its end locations (ending date and time). Three different number of vehicles (K=1,2 or 4) are considered (see file Vehicle data D-X-Y.csv). These values are based on real-case scenarios of a transportation company with its headquarter in the east of the Netherlands. Note that the starting date of the model has been set to 05-02-2024.

Order data consists of the number of orders from which a selection needs to be made, the identification number of each order, pickup and delivery dates, number of consecutive days (with respect to the pickup or delivery date) during which pickup/delivery is (also) allowed, pickup and delivery locations (country and zip code) and time window(s) (identical in case of multiple pickup/delivery days), the number of kilometers between the pickup and delivery location, the revenue earned when the order is selected, the demand (in LDMs) and weight of the order and whether the offering company requires the exchange of pallets and other auxiliary transport materials. Four different numbers of orders are used, with values N=25, 50, 100 or 250. Given the number of vehicles and orders, there are 3 x 4 = 12 data instances. Each instance is labeled as D-X-Y, where D denotes the data instance, X represents the number of vehicles, and Y indicates the number of orders. Notably, instances with the same number of orders share the same set of orders (e.g., D-1-25, D-2-25, and D-4-25 use identical orders). However, when the number of orders increases, a new set of orders is generated (e.g., the orders in D-1-25, D-1-50, D-4-100, and D-4-250 are distinct).

Additionally to the real-case instances, we also adapted instances from the literature for validation. Hence, we took 16 instances from El Bouyahyiouy and Bellabdaoui (2022), as the problem studied in that paper resembles the SMDPDPMTWPD. The instances in El Bouyahyiouy and Bellabdaoui (2022) are labeled as SFTa-bc-d-e, where: a is the instance number, b depicts the instance generation method (R, C and RC), c defines the number of orders in the order pool, d represents the number of trucks, and e shows the number of orders. In contrast to El Bouyahyiouy and Bellabdaoui (2022), the SMDPDPMTWPD studied in this paper allows trucks to travel directly from the starting depot to the ending depot when no positive revenue can be obtained from picking up and delivering orders. Consequently, we replicated their approach to repair and adapt the instances for solving the SMDPDPMTWPD.

The following steps are taken in order to generate instances for this paper based on El Bouyahyiouy and Bellabdaoui (2022):
    - Each vehicle has one start and one end location, where each vehicle starts fully empty at time t = 0. The coordinates of the start and end locations are random on the interval X, Y in [0, 150] such that the distance between the locations is greater than or equal to 130.
    - The time at which each vehicle should be back at its end location is based on the formula
          e_{τ_{ki}'} = ceil*{1000 - U(0,1) * 300}   i in K   
   - For each instance, we:
        - Take the first c coordinates of the order pool of generation method b (available at http://web.cba.neu.edu/~msolomon/problems.htm).
        - From these orders, randomly select e pickup locations and e delivery locations, where the pickup location should be different from the delivery location and the first drawn pickup location is coupled to the first drawn delivery location, etc.
        - Travel distances are calculated as the Euclidean distance between two locations. Travel costs are calculated from travel distances as mentioned in the paper, where night rest and pause breaks are ignored.
        - The profit, demand and weight of each order are calculated as before.
        - Service times and with of each time window (WTW) is taken from the El Bouyahyiouy and Bellabdaoui (2022).
        - The following formulas are used for the time windows:
              e_{i} = U(0.75,1.25) * min_{k in K}(t_(τ_{k}i})   i in P 
              l_{i} = e_{i} + WTW                               i in P
              e_{N+i} = e_{i} + s_{i} + U(1,2) * t_{i(N+i)}     i in D
              l_{N+i} = e_{N+i} + WTW                           i in D
