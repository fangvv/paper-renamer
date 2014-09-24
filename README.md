# README #

This is a Bash shell script created by Weiwei Fang. It is used to rename the academic paper files in pdf with the paper titles, based on the approach proposed in [SciPlore Xtract: Extracting Titles from Scientific PDF Documents by Analyzing Style Information (Font Size)](http://www.sciplore.org/wp-content/papercite-data/pdf/beel10e.pdf).

# System Requirment #
* Linux system
* Bash
* pdftohtml (utility contained in [Poppler](http://poppler.freedesktop.org/releases.html))
* sed

# How it works #
Put the script into the folder, use chmod to make it executable (i.e., chmod 755 paperrenamer), and then execute it. After the work is done, check the report.txt for the changes.
```
1: xxx.pdf --> yyy.pdf
```
You may notice the number at the begining of each line, which means:
```
1: title extracted from "font=0"
2: title extracted from "font=1"
3: sorry, we can't rename it
```
However, not all pdf files can be renamed according to the titles, as pointed out by the paper [SciPlore Xtract: Extracting Titles from Scientific PDF Documents by Analyzing Style Information (Font Size)](http://www.sciplore.org/wp-content/papercite-data/pdf/beel10e.pdf). Sometimes, you have to rename some of them manually.

# Examples (Dataset: Infocom 2014)#
**The original files are like the following:**
```
fang@fang:~/testpdf$ ls
1569792175.pdf  1569805973.pdf  1569808115.pdf  1569809795.pdf  1569810933.pdf
1569793069.pdf  1569806127.pdf  1569808183.pdf  1569809807.pdf  1569810941.pdf
1569795681.pdf  1569806203.pdf  1569808317.pdf  1569809809.pdf  1569810951.pdf
1569796319.pdf  1569806221.pdf  1569808339.pdf  1569809815.pdf  1569810979.pdf
1569796629.pdf  1569806271.pdf  1569808399.pdf  1569809833.pdf  1569810989.pdf
1569798293.pdf  1569806299.pdf  1569808409.pdf  1569809871.pdf  1569811003.pdf
1569798793.pdf  1569806315.pdf  1569808431.pdf  1569809889.pdf  1569811009.pdf
1569798911.pdf  1569806319.pdf  1569808459.pdf  1569809897.pdf  1569811033.pdf
1569798921.pdf  1569806431.pdf  1569808475.pdf  1569809899.pdf  1569811045.pdf
1569799049.pdf  1569806443.pdf  1569808481.pdf  1569809929.pdf  1569811059.pdf
1569799527.pdf  1569806533.pdf  1569808493.pdf  1569809965.pdf  1569811067.pdf
1569799611.pdf  1569806559.pdf  1569808553.pdf  1569810017.pdf  1569811105.pdf
1569800117.pdf  1569806603.pdf  1569808619.pdf  1569810021.pdf  1569811127.pdf
1569800235.pdf  1569806659.pdf  1569808653.pdf  1569810029.pdf  1569811135.pdf
1569800467.pdf  1569806703.pdf  1569808659.pdf  1569810045.pdf  1569811143.pdf
1569800763.pdf  1569806709.pdf  1569808661.pdf  1569810053.pdf  1569811177.pdf
1569801359.pdf  1569806751.pdf  1569808673.pdf  1569810057.pdf  1569811185.pdf
1569801679.pdf  1569806845.pdf  1569808715.pdf  1569810061.pdf  1569811215.pdf
1569801843.pdf  1569806899.pdf  1569808751.pdf  1569810069.pdf  1569811223.pdf
1569802221.pdf  1569806903.pdf  1569808753.pdf  1569810075.pdf  1569811243.pdf
1569802237.pdf  1569806907.pdf  1569808813.pdf  1569810079.pdf  1569811263.pdf
1569802559.pdf  1569806913.pdf  1569808819.pdf  1569810091.pdf  1569811273.pdf
1569802653.pdf  1569806915.pdf  1569808833.pdf  1569810127.pdf  1569811277.pdf
1569802683.pdf  1569806919.pdf  1569808837.pdf  1569810133.pdf  1569811297.pdf
1569802807.pdf  1569806931.pdf  1569808861.pdf  1569810149.pdf  1569811321.pdf
1569802815.pdf  1569806945.pdf  1569808869.pdf  1569810171.pdf  1569811337.pdf
1569802973.pdf  1569806955.pdf  1569808899.pdf  1569810175.pdf  1569811345.pdf
1569803135.pdf  1569806981.pdf  1569808905.pdf  1569810181.pdf  1569811387.pdf
1569803215.pdf  1569807013.pdf  1569808967.pdf  1569810183.pdf  1569811399.pdf
1569803247.pdf  1569807017.pdf  1569809039.pdf  1569810193.pdf  1569811405.pdf
1569803811.pdf  1569807037.pdf  1569809047.pdf  1569810199.pdf  1569811431.pdf
1569803845.pdf  1569807057.pdf  1569809055.pdf  1569810241.pdf  1569811433.pdf
1569803949.pdf  1569807061.pdf  1569809063.pdf  1569810269.pdf  1569811501.pdf
1569804011.pdf  1569807097.pdf  1569809085.pdf  1569810293.pdf  1569811533.pdf
1569804013.pdf  1569807119.pdf  1569809099.pdf  1569810305.pdf  1569811549.pdf
1569804231.pdf  1569807161.pdf  1569809107.pdf  1569810337.pdf  1569811569.pdf
1569804393.pdf  1569807189.pdf  1569809139.pdf  1569810349.pdf  1569811575.pdf
1569804585.pdf  1569807211.pdf  1569809151.pdf  1569810379.pdf  1569811661.pdf
1569804645.pdf  1569807293.pdf  1569809163.pdf  1569810409.pdf  1569811665.pdf
1569804715.pdf  1569807345.pdf  1569809191.pdf  1569810411.pdf  1569811675.pdf
1569805007.pdf  1569807415.pdf  1569809205.pdf  1569810423.pdf  1569811689.pdf
1569805047.pdf  1569807417.pdf  1569809263.pdf  1569810431.pdf  1569811709.pdf
1569805175.pdf  1569807435.pdf  1569809265.pdf  1569810439.pdf  1569811737.pdf
1569805181.pdf  1569807521.pdf  1569809271.pdf  1569810457.pdf  1569811753.pdf
1569805187.pdf  1569807523.pdf  1569809305.pdf  1569810465.pdf  1569811761.pdf
1569805191.pdf  1569807565.pdf  1569809355.pdf  1569810503.pdf  1569811771.pdf
1569805217.pdf  1569807591.pdf  1569809357.pdf  1569810513.pdf  1569811811.pdf
1569805231.pdf  1569807593.pdf  1569809377.pdf  1569810547.pdf  1569811835.pdf
1569805283.pdf  1569807599.pdf  1569809383.pdf  1569810581.pdf  1569811839.pdf
1569805517.pdf  1569807649.pdf  1569809405.pdf  1569810593.pdf  1569811857.pdf
1569805545.pdf  1569807655.pdf  1569809481.pdf  1569810599.pdf  1569811867.pdf
1569805581.pdf  1569807659.pdf  1569809483.pdf  1569810613.pdf  1569811891.pdf
1569805599.pdf  1569807673.pdf  1569809557.pdf  1569810647.pdf  1569811925.pdf
1569805617.pdf  1569807675.pdf  1569809579.pdf  1569810651.pdf  1569811969.pdf
1569805631.pdf  1569807749.pdf  1569809593.pdf  1569810679.pdf  1569811981.pdf
1569805709.pdf  1569807777.pdf  1569809615.pdf  1569810737.pdf  1569811993.pdf
1569805721.pdf  1569807829.pdf  1569809681.pdf  1569810763.pdf  1569812027.pdf
1569805733.pdf  1569807839.pdf  1569809701.pdf  1569810777.pdf  1569812071.pdf
1569805747.pdf  1569807853.pdf  1569809733.pdf  1569810785.pdf  1569812087.pdf
1569805775.pdf  1569807859.pdf  1569809737.pdf  1569810835.pdf  1569812089.pdf
1569805905.pdf  1569807919.pdf  1569809745.pdf  1569810887.pdf  1569812185.pdf
1569805925.pdf  1569807931.pdf  1569809769.pdf  1569810909.pdf  1569812585.pdf
1569805927.pdf  1569807979.pdf  1569809785.pdf  1569810915.pdf  1569812593.pdf
1569805945.pdf  1569807987.pdf  1569809789.pdf  1569810927.pdf  paperrenamer
```
**When the script runs:**
```
fang@fang:~/testpdf$ ./paperrenamer 
Process...............................................................................................................................................................................................................................................................................................................................Done

```
**The report file**
```
1: 1569792175.pdf --> PROMISE:_A_Framework_for_Truthful_and_Profit_Maximizing_Spectrum_Double_Auctions_.pdf
1: 1569793069.pdf --> Proactive_Fault-Tolerant_Aggregation_Protocol_for_Privacy-Assured_Smart_Metering_.pdf
1: 1569795681.pdf --> Efficiently_Collecting_Histograms_Over_RFID_Tags_.pdf
1: 1569796319.pdf --> 978-1-4799-3360-0_14_$31.00_c_2014_IEEE_.pdf
1: 1569796629.pdf --> Privacy-Preserving_Multi-Keyword_Fuzzy_Search_over_Encrypted_Data_in_the_Cloud_.pdf
1: 1569798293.pdf --> SimCast:_Efficient_Video_Delivery_in_MU-MIMO_WLANs_.pdf
1: 1569798793.pdf --> Near-Pri:_Private,_Proximity_Based_Location_Sharing_.pdf
1: 1569798911.pdf --> TOFEC:_Achieving_Optimal_Throughput-Delay_Trade-off_of_Cloud_Storage_Using_Erasure_Codes_.pdf
1: 1569798921.pdf --> A_Deep_Investigation_Into_Network_Performance_in_Virtual_Machine_Based_Cloud_Environments_.pdf
1: 1569799049.pdf --> Electronic_Frog_Eye:_Counting_Crowd_Using_WiFi_.pdf
1: 1569799527.pdf --> Shake_and_Walk:_Acoustic_Direction_Finding_and_Fine-grained_Indoor_Localization_Using_Smartphones_.pdf
1: 1569799611.pdf --> _*_§_*_*_*_*_*_*_*_§_IEEE_INFOCOM_2014_-_IEEE_Conference_on_Computer_Communications_978-14799-3360-0_14_$31.00_©2014_IEEE_.pdf
1: 1569800117.pdf --> Privacy-Preserving_High-Quality_Map_Generation_with_Participatory_Sensing_.pdf
1: 1569800235.pdf --> How_to_Crowdsource_Tasks_Truthfully_without_Sacrificing_Utility:_Online_Incentive_Mechanisms_with_Budget_Constraint_.pdf
1: 1569800467.pdf --> Open_Peering_by_Internet_Transit_Providers:_Peer_Preference_or_Peer_Pressure?_.pdf
1: 1569800763.pdf --> PS-TRUST:_Provably_Secure_Solution_for_Truthful_Double_Spectrum_Auctions_.pdf
1: 1569801359.pdf --> Geometric_Evaluation_of_Survivability_of_Disaster-affected_Network_with_Probabilistic_Failure_.pdf
1: 1569801679.pdf --> Multiple_Heterogeneous_Data_Ferry_Trajectory_Planning_in_Wireless_Sensor_Networks_.pdf
1: 1569801843.pdf --> New_Bandwidth_Sharing_and_Pricing_Policies_to_Achieve_A_Win-Win_Situation_for_Cloud_Provider_and_Tenants_.pdf
1: 1569802221.pdf --> Minimizing_Makespan_and_Total_Completion_Time_in_MapReduce-like_Systems_.pdf
1: 1569802237.pdf --> Optimal_CSMA-based_Wireless_Communication_with_Worst-case_Delay_and_Non-uniform_Sizes_.pdf
1: 1569802559.pdf --> Arbitrarily_Accurate_Approximation_Scheme_for_Large-Scale_RFID_Cardinality_Estimation_.pdf
1: 1569802653.pdf --> Information_Diffusion_in_Mobile_Social_Networks:_The_Speed_Perspective_.pdf
1: 1569802683.pdf --> Distributed_Stochastic_Optimization_via_Correlated_Scheduling_.pdf
1: 1569802807.pdf --> Efficient_Public_Integrity_Checking_for_Cloud_Data_Sharing_with_Multi-User_Modification_.pdf
1: 1569802815.pdf --> IEEE_INFOCOM_2014_-_IEEE_Conference_on_Computer_Communications_978-14799-3360-0_14_$31.00_©2014_IEEE_.pdf
1: 1569802973.pdf --> Keep_Forwarding:_Towards_K-link_Failure_Resilient_Routing_.pdf
1: 1569803135.pdf --> Improving_Data_Forwarding_in_Mobile_Social_Networks_with_Infrastructure_Support:_A_Space-Crossing_Community_Approach_.pdf
1: 1569803215.pdf --> Safe_Charging_for_Wireless_Power_Transfer_.pdf
1: 1569803247.pdf --> Incentivize_Cooperative_Sensing_in_Distributed_Cognitive_Radio_Networks_with_Reputation-based_Pricing_.pdf
1: 1569803811.pdf --> A_Stable_Fountain_Code_Mechanism_for_Peer-to-Peer_Content_Distribution_.pdf
1: 1569803845.pdf --> Dynamic_Resource_Provisioning_in_Cloud_Computing:_A_Randomized_Auction_Approach_.pdf
1: 1569803949.pdf --> TOSS:_Trafﬁc_Ofﬂoading_by_Social_Network_Service-Based_Opportunistic_Sharing_in_Mobile_Social_Networks_.pdf
1: 1569804011.pdf --> Hitchhike:_Riding_Control_on_Preambles_.pdf
1: 1569804013.pdf --> Walking_down_the_STAIRS:_Efﬁcient_Collision_Resolution_for_Wireless_Sensor_Networks_.pdf
1: 1569804231.pdf --> Throughput-Delay_Tradeoff_in_Mobile_Ad_Hoc_Networks_with_Correlated_Mobility_.pdf
1: 1569804393.pdf --> How_Can_Botnets_Cause_Storms?_Understanding_the_Evolution_and_Impact_of_Mobile_Botnets_.pdf
1: 1569804585.pdf --> Neptune:_Efficient_Remote_Communication_Services_for_Cloud_Backups_.pdf
1: 1569804645.pdf --> Towards_Adaptive_Continuous_Scanning_in_Large-Scale_RFID_Systems_.pdf
1: 1569804715.pdf --> WiSlow:_A_Wi-Fi_Network_Performance_Troubleshooting_Tool_for_End_Users_.pdf
1: 1569805007.pdf --> MIMO-based_Jamming_Resilient_Communication_in_Wireless_Networks_.pdf
1: 1569805047.pdf --> Restorable_Logical_Topology_in_the_Face_of_No_or_Partial_Traffic_Demand_Knowledge_.pdf
1: 1569805175.pdf --> Critical_Sensing_Range_for_Mobile_Heterogeneous_Camera_Sensor_Networks_.pdf
1: 1569805181.pdf --> Delay-Throughput_Tradeoff_with_Correlated_Mobility_of_Ad-Hoc_Networks_.pdf
1: 1569805187.pdf --> RIAL:_Resource_Intensity_Aware_Load_Balancing_in_Clouds_.pdf
1: 1569805191.pdf --> Consolidating_Complementary_VMs_with_Spatial_Temporal-awareness_in_Cloud_Datacenters_.pdf
1: 1569805217.pdf --> DSearching:_Distributed_Searching_of_Mobile_Nodes_in_DTNs_with_Floating_Mobility_Information_.pdf
1: 1569805231.pdf --> Epidemic_Thresholds_with_External_Agents_.pdf
1: 1569805283.pdf --> Fast_Resource_Scheduling_in_HetNets_with_D2D_Support_.pdf
1: 1569805517.pdf --> An_Approximation_Algorithm_for_Client_Assignment_in_Client_Server_Systems_.pdf
1: 1569805545.pdf --> On_Diagnosis_of_Forwarding_Plane_via_Static_Forwarding_Rules_in_Software_Deﬁned_Networks_.pdf
1: 1569805581.pdf --> Multi-Dimensional_OFDMA_Scheduling_in_a_Wireless_Network_with_Relay_Nodes_.pdf
1: 1569805599.pdf --> Bounded_Stretch_Geographic_Homotopic_Routing_in_Sensor_Networks_.pdf
1: 1569805617.pdf --> SBVLC:_Secure_Barcode-based_Visible_Light_Communication_for_Smartphones_.pdf
1: 1569805631.pdf --> How_to_identify_global_trends_from_local_decisions?_Event_Region_Detection_on_Mobile_Networks_.pdf
1: 1569805709.pdf --> Sleep_in_the_Dins:_Insomnia_Therapy_for_Duty-cycled_Sensor_Networks_.pdf
1: 1569805721.pdf --> _.pdf
1: 1569805733.pdf --> Joint_Scheduling_of_MapReduce_Jobs_with_Servers:_Performance_Bounds_and_Experiments_.pdf
1: 1569805747.pdf --> Scaling_Laws_for_Heterogeneous_Cognitive_Radio_Networks_with_Cooperative_Secondary_Users_.pdf
3: 1569805775.pdf
1: 1569805905.pdf --> Sojourn_time_approximations_in_a_multi-class_time-sharing_server_.pdf
1: 1569805925.pdf --> Anchor-free_Backscatter_Positioning_for_RFID_Tags_with_High_Accuracy_.pdf
1: 1569805927.pdf --> RollCaller:_User-Friendly_Indoor_Navigation_System_Using_Human-Item_Spatial_Relation_.pdf
1: 1569805945.pdf --> 01_234546741_849__22
_4__3_4__2_.pdf
1: 1569805973.pdf --> Software_Defined_Monitoring_of_Application_Protocols_.pdf
1: 1569806127.pdf --> 1_1_.pdf
1: 1569806203.pdf --> A_Cooperative_Advanced_Driver_Assistance_System_to_Mitigate_Vehicular_Traffic_Shock_Waves_.pdf
2: 1569806221.pdf --> Optimal_Collaborative_Access_Point_Association_in_Wireless_Networks_.pdf
1: 1569806271.pdf --> Data-driven_Trafﬁc_Flow_Analysis_for_Vehicular_Communications_.pdf
1: 1569806299.pdf --> On_the_Geographic_Patterns_of_a_Large-scale_Mobile_Video-on-Demand_System_.pdf
1: 1569806315.pdf --> 3D_Pipeline_Contention:_Asymmetric_Full_Duplex_in_Wireless_Networks_.pdf
2: 1569806319.pdf --> CACH:_Cycle-Adjustable_Channel_Hopping_for_Control_Channel_Establishment_in_Cognitive_Radio_Networks_.pdf
1: 1569806431.pdf --> Read_Bulk_Data_from_Computational_RFIDs_.pdf
1: 1569806443.pdf --> A_unified_approach_to_the_performance_analysis_of_caching_systems_.pdf
1: 1569806533.pdf --> COLLECTOR:_A_Secure_RFID-Enabled_Batch_Recall_Protocol_.pdf
1: 1569806559.pdf --> INDAPSON:_An_Incentive_Data_Plan_Sharing_System_Based_on_Self-Organizing_Network_.pdf
1: 1569806603.pdf --> Maximizing_the_Number_of_Satisfied_Subscribers_in_Pub_Sub_Systems_Under_Capacity_Constraints_.pdf
1: 1569806659.pdf --> CityDrive:_A_Map-Generating_and_Speed-Optimizing_Driving_System_.pdf
1: 1569806703.pdf --> When_Queueing_Meets_Coding:_Optimal-Latency_Data_Retrieving_Scheme_in_Storage_Clouds_.pdf
1: 1569806709.pdf --> 1_.pdf
1: 1569806751.pdf --> Montage:_Combine_Frames_with_Movement_Continuity_for_Realtime_Multi-User_Tracking_.pdf
1: 1569806845.pdf --> Energy-efﬁcient_Cooperative_Broadcast_in_Fading_Wireless_Networks_.pdf
1: 1569806899.pdf --> Power_Consumption_of_Virtual_Machines_with_Network_Transactions:_Measurement_and_Improvements_.pdf
1: 1569806903.pdf --> Can_Mobile_Cloudlets_Support_Mobile_Applications?_.pdf
1: 1569806907.pdf --> Optimizing_Offline_Access_to_Social_Network_Content_on_Mobile_Devices_.pdf
1: 1569806913.pdf --> :_Embracing_Device-to-Device_Communication_.pdf
1: 1569806915.pdf --> A_Privacy-aware_Cloud-assisted_Healthcare_Monitoring_System_via_Compressive_Sensing_.pdf
1: 1569806919.pdf --> Multi-lateral_Privacy-Preserving_Localization_in_Pervasive_Environments_.pdf
1: 1569806931.pdf --> Sonar_Inside_Your_Body:_Prototyping_Ultrasonic_Intra-body_Sensor_Networks_.pdf
1: 1569806945.pdf --> TOC:_Localizing_Wireless_Rechargeable_Sensors_with_Time_of_Charge_.pdf
1: 1569806955.pdf --> Robust_Uncoded_Video_Transmission_over_Wireless_Fast_Fading_Channel_.pdf
3: 1569806981.pdf
1: 1569807013.pdf --> A_Stochastic_Game_for_Privacy_Preserving_Context_Sensing_on_Mobile_Phone_.pdf
1: 1569807017.pdf --> Achieving_Differential_Privacy_of_Data_Disclosure_in_the_Smart_Grid_.pdf
1: 1569807037.pdf --> Scalable_User_Selection_for_MU-MIMO_Networks_.pdf
1: 1569807057.pdf --> ForeSight:_Mapping_Vehicles_in_Visual_Domain_and_Electronic_Domain_.pdf
1: 1569807061.pdf --> Max-Flow_Min-Cut_Theorem_and_Faster_Algorithms_in_a_Circular_Disk_Failure_Model_.pdf
1: 1569807097.pdf --> Exploring_Bundling_Sale_Strategy_in_Online_Service_Markets_with_Network_Effects_.pdf
1: 1569807119.pdf --> Enabling_Crowd-Sourced_Mobile_Internet_Access_.pdf
1: 1569807161.pdf --> Online_Load_Balancing_for_MapReduce_with_Skewed_Data_Input_.pdf
1: 1569807189.pdf --> Hybrid_Data_Pricing_for_Network-Assisted_User-Provided_Connectivity_.pdf
1: 1569807211.pdf --> Performance-aware_Energy_Optimization_on_Mobile_Devices_in_Cellular_Network_.pdf
1: 1569807293.pdf --> LiFi:_Line-Of-Sight_Identiﬁcation_with_WiFi_.pdf
1: 1569807345.pdf --> Information_Leaks_Out:_Attacks_and_Countermeasures_on_Compressive_Data_Gathering_in_Wireless_Sensor_Networks_.pdf
1: 1569807415.pdf --> Multi-Terabyte_and_Multi-Gbps_Information_Centric_Routers_.pdf
1: 1569807417.pdf --> On_the_effect_of_forwarding_table_size_on_SDN_network_utilization_.pdf
1: 1569807435.pdf --> Practical_DCB_for_Improved_Data_Center_Networks_.pdf
1: 1569807521.pdf --> Secure_Cooperative_Spectrum_Sensing_and_Access_Against_Intelligent_Malicious_Behaviors_.pdf
1: 1569807523.pdf --> EasyBid:_Enabling_Cellular_Offloading_via_Small_Players_.pdf
1: 1569807565.pdf --> A_Social_Group_Utility_Maximization_Framework_with_Applications_in_Database_Assisted_Spectrum_Access_.pdf
1: 1569807591.pdf --> Connected_Wireless_Camera_Network_Deployment_with_Visibility_Coverage_.pdf
1: 1569807593.pdf --> kBF:_a_Bloom_Filter_for_Key-Value_Storage_with_an_Application_on_Approximate_State_Machines_.pdf
1: 1569807599.pdf --> Heat-Diffusion:_Pareto_Optimal_Dynamic_Routing_for_Time-Varying_Wireless_Networks_.pdf
1: 1569807649.pdf --> Cooperative_Cross-Technology_Interference_Mitigation_for_Heterogeneous_Multi-hop_Networks_.pdf
1: 1569807655.pdf --> Detecting_Malicious_HTTP_Redirections_Using_Trees_of_User_Browsing_Activity_.pdf
1: 1569807659.pdf --> Optimal_Link_Scheduling_for_Delay-constrained_Periodic_Traffic_over_Unreliable_Wireless_Links_.pdf
1: 1569807673.pdf --> Approximate_Multiple_Count_in_Wireless_Sensor_Networks_.pdf
1: 1569807675.pdf --> A_Robust_Information_Source_Estimator_with_Sparse_Observations_.pdf
1: 1569807749.pdf --> 978-1-4799-3360-0_14_$31.00_©2014_IEEE_.pdf
1: 1569807777.pdf --> Time_Dependent_Pricing_in_Wireless_Data_Networks:_Flat-Rate_vs._Usage-Based_Schemes_.pdf
1: 1569807829.pdf --> TRAC:_Truthful_Auction_for_Location-Aware_Collaborative_Sensing_in_Mobile_Crowdsourcing_.pdf
1: 1569807839.pdf --> Double_Auctions_for_Dynamic_Spectrum_Allocation_.pdf
1: 1569807853.pdf --> Fair_Energy-efﬁcient_Sensing_Task_Allocation_in_Participatory_Sensing_with_Smartphones_.pdf
1: 1569807859.pdf --> Bloom_Tree:_A_Search_Tree_Based_on_Bloom_Filters_for_Multiple-Set_Membership_Testing_.pdf
1: 1569807919.pdf --> Signaling_Free_Localization_of_Node_Failures_in_All-Optical_Networks_.pdf
1: 1569807931.pdf --> FD-MMAC:_Combating_Multi-Channel_Hidden_and_Exposed_Terminals_Using_a_Single_Transceiver_.pdf
1: 1569807979.pdf --> Optimal_Approximation_Algorithm_of_Virtual_Machine_Placement_for_Data_Latency_Minimization_in_Cloud_Systems_.pdf
1: 1569807987.pdf --> Automated_Dynamic_Offset_Applied_to_Cell_Association_.pdf
1: 1569808115.pdf --> Improved_Structures_for_Data_Collection_in_Wireless_Sensor_Networks_.pdf
1: 1569808183.pdf --> Spatio-temporal_Factorization_of_Log_Data_for_Understanding_Network_Events_.pdf
1: 1569808317.pdf --> 1_•_•_•_.pdf
1: 1569808339.pdf --> Blowing_Hard_Is_Not_All_We_Want:_Quantity_vs_Quality_of_Wind_Power_in_the_Smart_Grid_.pdf
1: 1569808399.pdf --> A_longitudinal_analysis_of_Internet_rate_limitations_.pdf
1: 1569808409.pdf --> Analysis_and_Detection_of_SIMbox_Fraud_in_Mobility_Networks_.pdf
1: 1569808431.pdf --> Monitor_Placement_for_Maximal_Identifiability_in_Network_Tomography_.pdf
2: 1569808459.pdf --> Dynamic_Speed_Scaling_for_Energy_Minimization_in_Delay-Tolerant_Smartphone_Applications_.pdf
1: 1569808475.pdf --> Competitive_MAC_under_Adversarial_SINR_.pdf
1: 1569808481.pdf --> Scaling_Laws_for_Secrecy_Capacity_in_Cooperative_Wireless_Networks_.pdf
1: 1569808493.pdf --> Optimal_Rate_Sampling_in_802.11_Systems_.pdf
1: 1569808553.pdf --> Fault_Tolerant_Barrier_Coverage_for_Wireless_Sensor_Networks_.pdf
2: 1569808619.pdf --> Personal_Clouds:_Sharing_and_Integrating_Networked_Resources_to_Enhance_End_User_Experiences_.pdf
1: 1569808653.pdf --> A_Credit-Token-Based_Spectrum_Etiquette_Framework_for_Coexistence_of_Heterogeneous_Cognitive_Radio_Networks_.pdf
2: 1569808659.pdf --> —Opportunistic_trafﬁc_ofﬂoading_has_been_proposed_.pdf
2: 1569808661.pdf --> iBeam:_Intelligent_Client-Side_Multi-User_Beamforming_in_Wireless_Networks_.pdf
1: 1569808673.pdf --> Energy-Efﬁcient_Capacity_Optimization_in_Wireless_Networks_.pdf
1: 1569808715.pdf --> Optimal_Rate_Allocation_for_Adaptive_Wireless_Video_Streaming_in_Networks_with_User_Dynamics_.pdf
1: 1569808751.pdf --> Distributed_Data_Storage_Systems_with_Opportunistic_Repair_.pdf
1: 1569808753.pdf --> Scalable_Pending_Interest_Table_Design:_From_Principles_to_Practice_.pdf
1: 1569808813.pdf --> NOVA:_QoE-driven_Optimization_of_DASH-based_Video_Delivery_in_Networks_.pdf
1: 1569808819.pdf --> Robust_and_Cost-Effective_Architecture_Design_for_Smart_Grid_Communications:_A_Multi-stage_Middleware_Deployment_Approach_.pdf
1: 1569808833.pdf --> Joint_Power_Optimization_of_Data_Center_Network_and_Servers_with_Correlation_Analysis_.pdf
1: 1569808837.pdf --> Venice:_Reliable_Virtual_Data_Center_Embedding_in_Clouds_.pdf
1: 1569808861.pdf --> Modeling_Social_Network_Relationships_via_t-Cherry_Junction_Trees_.pdf
1: 1569808869.pdf --> “Can_you_SEE_me_now?”_A_Measurement_Study_of_Mobile_Video_Calls_.pdf
1: 1569808899.pdf --> Towards_Zero-Time_Wakeup_of_Line_Cards_in_Power-Aware_Routers_.pdf
1: 1569808905.pdf --> SoCast:_Social_Ties_Based_Cooperative_Video_Multicast_.pdf
1: 1569808967.pdf --> ShopProﬁler:_Proﬁling_Shops_with_Crowdsourcing_Data_.pdf
1: 1569809039.pdf --> TorWard:_Discovery_of_Malicious_Traffic_over_Tor_.pdf
1: 1569809047.pdf --> REIN:_A_Fast_Event_Matching_Approach_for_Content-based_Publish_Subscribe_Systems_.pdf
1: 1569809055.pdf --> Application-Level_Scheduling_with_Deadline_Constraints_.pdf
1: 1569809063.pdf --> 3D_Surface_Localization_with_Terrain_Model_.pdf
1: 1569809085.pdf --> Reliable_Video_Multicast_over_Wi-Fi_Networks_with_Coordinated_Multiple_APs_.pdf
1: 1569809099.pdf --> LBSNSim:_Analyzing_and_Modeling_Location-based_Social_Networks_.pdf
1: 1569809107.pdf --> A_Uniﬁed_Framework_for_Wireless_Max-Min_Utility_Optimization_with_General_Monotonic_Constraints_.pdf
1: 1569809139.pdf --> Does_Full-Duplex_Double_the_Capacity_of_Wireless_Networks?_.pdf
1: 1569809151.pdf --> Towards_Automatic_Phone-to-Phone_Communication_for_Vehicular_Networking_Applications_.pdf
1: 1569809163.pdf --> Software_Defined_Green_Data_Center_Network_with_Exclusive_Routing_.pdf
1: 1569809191.pdf --> Mining_Checkins_from_Location-sharing_Services_for_Client-independent_IP_Geolocation_.pdf
1: 1569809205.pdf --> A_Generalized_Coverage-Preserving_Scheduling_in_WSNs:_a_Case_Study_in_Structural_Health_Monitoring_.pdf
1: 1569809263.pdf --> Toward_Profit-Seeking_Virtual_Network_Embedding_Algorithm_via_Global_Resource_Capacity_.pdf
1: 1569809265.pdf --> Contextual_Localization_Through_Network_Traffic_Analysis_.pdf
1: 1569809271.pdf --> Performance_Evaluation_and_Asymptotics_for_Content_Delivery_Networks_.pdf
1: 1569809305.pdf --> Heterogeneity-Aware_Data_Regeneration_in_Distributed_Storage_Systems_.pdf
1: 1569809355.pdf --> Joint_Online_Transcoding_and_Geo-distributed_Delivery_for_Dynamic_Adaptive_Streaming_.pdf
1: 1569809357.pdf --> Enabling_Efficient_Access_Control_with_Dynamic_Policy_Updating_for_Big_Data_in_the_Cloud_.pdf
1: 1569809377.pdf --> Classifying_Call_Profiles_in_Large-scale_Mobile_Traffic_Datasets_.pdf
1: 1569809383.pdf --> HadoopWatch:_A_First_Step_Towards_Comprehensive_Traffic_Forecasting_in_Cloud_Computing_.pdf
1: 1569809405.pdf --> Reducing_Forwarding_State_in_Content-Centric_Networks_with_Semi-Stateless_Forwarding_.pdf
1: 1569809481.pdf --> Using_Stop-and-Wait_to_Improve_TCP_Throughput_in_Fast_Optical_Switching_(FOS)_Networks_over_Short_Physical_Distances_.pdf
1: 1569809483.pdf --> On_the_Expected_Size_of_Minimum-Energy_Path-preserving_Topologies_for_Wireless_Multi-hop_Networks_.pdf
1: 1569809557.pdf --> Mobile_Offloading_in_the_Wild:_Findings_and_Lessons_Learned_Through_a_Real-life_Experiment_with_a_New_Cloud-aware_System_.pdf
1: 1569809579.pdf --> CauseInfer_:Automatic_and_Distributed_Performance_Diagnosis_with_Hierarchical_Causality_Graph_in_Large_Distributed_Systems_.pdf
1: 1569809593.pdf --> Sharp_Per-Flow_Delay_Bounds_for_Bursty_Arrivals:_The_Case_of_FIFO,_SP,_and_EDF_Scheduling_.pdf
1: 1569809615.pdf --> Achieving_Privacy_Preservation_in_WiFi_Fingerprint-Based_Localization_.pdf
1: 1569809681.pdf --> A_Practical_Self-Adaptive_Rendezvous_Protocol_in_Cognitive_Radio_Ad_Hoc_Networks_.pdf
1: 1569809701.pdf --> EV-Sounding:_A_Visual_Assisted_Electronic_Channel_Sounding_System_.pdf
1: 1569809733.pdf --> Efficient_Distributed_Query_Processing_in_Large_RFID-enabled_Supply_Chains_.pdf
1: 1569809737.pdf --> Safe_Routing_Reconfigurations_with_Route_Redistribution_.pdf
1: 1569809745.pdf --> On_Efficient_Bandwidth_Allocation_for_Traffic_Variability_in_Datacenters_.pdf
1: 1569809769.pdf --> RepFlow:_Minimizing_Flow_Completion_Times_with_Replicated_Flows_in_Data_Centers_.pdf
1: 1569809785.pdf --> Pandaka:_A_Lightweight_Cipher_for_RFID_Systems_.pdf
1: 1569809789.pdf --> Dynamic_Pricing_and_Proﬁt_Maximization_for_the_Cloud_with_Geo-distributed_Data_Centers_.pdf
1: 1569809795.pdf --> Intelligent_SDN_based_Traffic_(de)Aggregation_and_Measurement_Paradigm_(iSTAMP)_.pdf
1: 1569809807.pdf --> From_Least_Interference-Cost_Paths_to_Maximum_(Concurrent)_Multiflow_in_MC-MR_Wireless_Networks_.pdf
1: 1569809809.pdf --> Distributed_Backup_Scheduling:_Modeling_and_Optimization_.pdf
1: 1569809815.pdf --> Fast_And_Simple_Approximation_Algorithms_for_Maximum_Weighted_Independent_Set_of_Links_.pdf
1: 1569809833.pdf --> Scalable_Forwarding_Tables_for_Supporting_Flexible_Policies_in_Enterprise_Networks_.pdf
1: 1569809871.pdf --> Multirate_Multicast:_Optimal_Algorithms_and_Implementation_.pdf
1: 1569809889.pdf --> A_High-order_Markov_Chain_Based_Scheduling_Algorithm_for_Low_Delay_in_CSMA_Networks_.pdf
1: 1569809897.pdf --> Delay-Constrained_Caching_in_Cognitive_Radio_Networks_.pdf
1: 1569809899.pdf --> Spectrum-Aware_Data_Replication_in_Intermittently_Connected_Cognitive_Radio_Networks_.pdf
1: 1569809929.pdf --> Optimal_Privacy-Preserving_Energy_Management_for_Smart_Meters_.pdf
1: 1569809965.pdf --> Learning_in_Hide-and-Seek_.pdf
1: 1569810017.pdf --> Dynamic_Content_Allocation_for_Cloud-assisted_Service_of_Periodic_Workloads_.pdf
3: 1569810021.pdf
1: 1569810029.pdf --> Characterizing_the_Achievable_Throughput_in_Wireless_Networks_with_Two_Active_RF_chains_.pdf
1: 1569810045.pdf --> Transductive_Malware_Label_Propagation:_Find_Your_Lineage_From_Your_Neighbors_.pdf
1: 1569810053.pdf --> SYNERGY:_A_Game-Theoretical_Approach_for_Cooperative_Key_Generation_in_Wireless_Networks_.pdf
1: 1569810057.pdf --> A_General_Framework_of_Hybrid_Graph_Sampling_for_Complex_Network_Analysis_.pdf
1: 1569810061.pdf --> Multi-Objective_Data_Placement_for_Multi-Cloud_Socially_Aware_Services_.pdf
1: 1569810069.pdf --> Video_Delivery_over_Heterogeneous_Cellular_Networks:_Optimizing_Cost_and_Performance_.pdf
1: 1569810075.pdf --> Cross-Layer_Path_Management_in_Multi-path_Transport_Protocol_for_Mobile_Devices_.pdf
1: 1569810079.pdf --> Traffic_Engineering_with_Equal-Cost-MultiPath:_An_Algorithmic_Perspective_.pdf
1: 1569810091.pdf --> Loss_Differentiation:_Moving_onto_High-Speed_Wireless_LANs_.pdf
1: 1569810127.pdf --> Microeconomic_Analysis_of_Base-Station_Sharing_in_Green_Cellular_Networks_.pdf
1: 1569810133.pdf --> Cell_Planning_for_Heterogeneous_Networks:_An_Approximation_Algorithm_.pdf
1: 1569810149.pdf --> Separating_Wheat_from_Chaff:_Winnowing_Unintended_Prefixes_using_Machine_Learning_.pdf
1: 1569810171.pdf --> Aggrecode:_Constructing_Route_Intersection_for_Data_Reconstruction_in_Erasure_Coded_Storage_.pdf
1: 1569810175.pdf --> Utility-based_Cooperative_Decision_in_Cooperative_Authentication_.pdf
1: 1569810181.pdf --> Meeting_Service_Level_Agreement_Cost-Effectively_for_Video-on-Demand_Applications_in_the_Cloud_.pdf
1: 1569810183.pdf --> Distributed_Opportunistic_Scheduling_for_Wireless_Networks_Powered_by_Renewable_Energy_Sources_.pdf
1: 1569810193.pdf --> Protecting_Your_Right:_Attribute-based_Keyword_Search_with_Fine-grained_Owner-enforced_Search_Authorization_in_the_Cloud_.pdf
1: 1569810199.pdf --> Is_it_Worth_to_be_Patient?_Analysis_and_Optimization_of_Delayed_Mobile_Data_Offloading_.pdf
1: 1569810241.pdf --> A_College_Admissions_Game_for_Uplink_User_Association_in_Wireless_Small_Cell_Networks_.pdf
1: 1569810269.pdf --> Forwarding_Redundancy_in_Opportunistic_Mobile_Networks:_Investigation_and_Elimination_.pdf
1: 1569810293.pdf --> BlueID:_A_Practical_System_for_Bluetooth_Device_Identification_.pdf
1: 1569810305.pdf --> Beyond_the_MDS_Bound_in_Distributed_Cloud_Storage_.pdf
1: 1569810337.pdf --> Achieving_k-anonymity_in_Privacy-Aware_Location-Based_Services_.pdf
1: 1569810349.pdf --> Greenbench:_A_Benchmark_for_Observing_Power_Grid_Vulnerability_Under_Data-Centric_Threats_.pdf
1: 1569810379.pdf --> Rendezvous_for_Heterogeneous_Spectrum-Agile_Devices_.pdf
3: 1569810409.pdf
1: 1569810411.pdf --> Online_Algorithms_for_Uploading_Deferrable_Big_Data_to_The_Cloud_.pdf
1: 1569810423.pdf --> Towards_Ubiquitous_Indoor_Localization_Service_Leveraging_Environmental_Physical_Features_.pdf
1: 1569810431.pdf --> POST:_Exploiting_Dynamic_Sociality_for_Mobile_Advertising_in_Vehicular_Networks_.pdf
1: 1569810439.pdf --> Scheduling_of_Multicast_and_Unicast_Services_under_Limited_Feedback_by_using_Rateless_Codes_.pdf
3: 1569810457.pdf
1: 1569810465.pdf --> Cooperative_Repair_with_Minimum-Storage_Regenerating_Codes_for_Distributed_Storage_.pdf
2: 1569810503.pdf --> Delay_Guaranteed_Live_Migration_of_Virtual_Machines_.pdf
1: 1569810513.pdf --> Joint_Static_and_Dynamic_Traffic_Scheduling_in_Data_Center_Networks_.pdf
1: 1569810547.pdf --> WiFall:_Device-free_Fall_Detection_by_Wireless_Networks_.pdf
1: 1569810581.pdf --> “Wireless_Networks_Without_Edges”:_Dynamic_Radio_Resource_Clustering_and_User_Scheduling_.pdf
1: 1569810593.pdf --> SenSpeed:_Sensing_Driving_Conditions_to_Estimate_Vehicle_Speed_in_Urban_Environments_.pdf
1: 1569810599.pdf --> An_Optimal_Data_Collection_Technique_for_Improved_Utility_in_UAS-aided_Networks_.pdf
1: 1569810613.pdf --> Will_Cyber-Insurance_Improve_Network_Security?_A_Market_Analysis_.pdf
1: 1569810647.pdf --> Distributed_Learning_for_Utility_Maximization_over_CSMA-based_Wireless_Multihop_Networks_.pdf
1: 1569810651.pdf --> Trade-offs_in_Optimizing_the_Cache_Deployments_of_CDNs_.pdf
1: 1569810679.pdf --> Cellular_Multi-Coverage_with_Non-uniform_Rates_.pdf
1: 1569810737.pdf --> Flexauc:_Serving_Dynamic_Demands_in_Spectrum_Trading_Markets_with_Flexible_Auction_.pdf
1: 1569810763.pdf --> Packet_Classiﬁcation_Using_Binary_Content_Addressable_Memory_.pdf
1: 1569810777.pdf --> An_Overlay_Automata_Approach_to_Regular_Expression_Matching_.pdf
1: 1569810785.pdf --> LD-Sketch:_A_Distributed_Sketching_Design_for_Accurate_and_Scalable_Anomaly_Detection_in_Network_Data_Streams_.pdf
1: 1569810835.pdf --> Provable_Per-Link_Delay-Optimal_CSMA_for_General_Wireless_Network_Topology_.pdf
1: 1569810887.pdf --> Maximizing_the_Value_of_Sensed_Information_in_Underwater_Wireless_Sensor_Networks_via_an_Autonomous_Underwater_Vehicle_.pdf
1: 1569810909.pdf --> Improving_mobile_video_streaming_with_link_aware_scheduling_and_client_caches_.pdf
1: 1569810915.pdf --> MISC:_Merging_Incorrect_Symbols_using_Constellation_Diversity_for_802.11_Retransmission_.pdf
1: 1569810927.pdf --> PLAM:_A_Privacy-Preserving_Framework_for_Local-Area_Mobile_Social_Networks_.pdf
1: 1569810933.pdf --> Profit-Maximizing_Incentive_for_Participatory_Sensing_.pdf
1: 1569810941.pdf --> FINE:_A_Fine-Grained_Privacy-Preserving_Location-based_Service_Framework_for_Mobile_Devices_.pdf
1: 1569810951.pdf --> Preserving_Secondary_Users’_Privacy_in_Cognitive_Radio_Networks_.pdf
1: 1569810979.pdf --> Enhancing_Zigbee_throughput_under_WiFi_interference_using_real-time_adaptive_coding_.pdf
1: 1569810989.pdf --> A_Reduction-based_Approach_Towards_Scaling_Up_Formal_Analysis_of_Internet_Configurations_.pdf
3: 1569811003.pdf
3: 1569811009.pdf
1: 1569811033.pdf --> Markov_Chain_Fingerprinting_to_Classify_Encrypted_Traffic_.pdf
1: 1569811045.pdf --> Robust_and_Optimal_Opportunistic_Scheduling_for_Downlink_2-Flow_Inter-session_Network_Coding_with_Varying_Channel_Quality_.pdf
1: 1569811059.pdf --> LP-relaxation_based_Distributed_Algorithms_for_Scheduling_in_Wireless_Networks_.pdf
1: 1569811067.pdf --> Hello:_A_Generic_Flexible_Protocol_for_Neighbor_Discovery_.pdf
1: 1569811105.pdf --> 1_3_3_3_3_3_3_3_.pdf
3: 1569811127.pdf
3: 1569811135.pdf
3: 1569811143.pdf
1: 1569811177.pdf --> Relax,_but_Do_Not_Sleep:_A_New_Perspective_on_Green_Wireless_Networking_.pdf
1: 1569811185.pdf --> Power_Grid_Vulnerability_to_Geographically_Correlated_Failures_–_Analysis_and_Control_Implications_.pdf
1: 1569811215.pdf --> VABKS:_Veriﬁable_Attribute-based_Keyword_Search_over_Outsourced_Encrypted_Data_.pdf
1: 1569811223.pdf --> SAP:_Similarity-Aware_Partitioning_for_Efficient_Cloud_Storage_.pdf
1: 1569811243.pdf --> Towards_a_System_Theoretic_Approach_to_Wireless_Network_Capacity_in_Finite_Time_and_Space_.pdf
1: 1569811263.pdf --> IP_Fast_Rerouting_for_Multi-Link_Failures_.pdf
1: 1569811273.pdf --> On_the_Catalyzing_Effect_of_Randomness_on_the_Per-Flow_Throughput_in_Wireless_Networks_.pdf
1: 1569811277.pdf --> Toward_Optimal_Allocation_of_Location_Dependent_Tasks_in_Crowdsensing_.pdf
1: 1569811297.pdf --> Probability_Distribution_of_Spectral_Hole_Duration_in_Cognitive_Networks_.pdf
1: 1569811321.pdf --> Let’s_Stay_Together:_Towards_Traffic_Aware_Virtual_Machine_Placement_in_Data_Centers_.pdf
1: 1569811337.pdf --> On_Designing_Neighbor_Discovery_Protocols:_A_Code-Based_Approach_.pdf
1: 1569811345.pdf --> Rate-Control_and_Multi-Channel_Scheduling_for_Wireless_Live_Streaming_with_Stringent_Deadlines_.pdf
1: 1569811387.pdf --> Routing_Games_with_Progressive_Filling_.pdf
3: 1569811399.pdf
1: 1569811405.pdf --> Rippler:_Delay_Injection_for_Service_Dependency_Detection_.pdf
1: 1569811431.pdf --> Cooperative_Anti-jamming_for_Infrastructure-less_Wireless_Networks_with_Stochastic_Relaying_.pdf
1: 1569811433.pdf --> Analysis_of_a_Proportionally_Fair_and_Locally_Adaptive_Spatial_Aloha_in_Poisson_Networks_.pdf
1: 1569811501.pdf --> Scheduling_Multicast_Traffic_with_Deadlines_in_Wireless_Networks_.pdf
1: 1569811533.pdf --> Restricted_Coverage_in_Wireless_Networks_.pdf
1: 1569811549.pdf --> Scheduling_Jobs_with_Dwindling_Resource_Requirements_in_Clouds_.pdf
1: 1569811569.pdf --> Assurable,_Transparent,_and_Mutual_Restraining_E-voting_Involving_Multiple_Conflicting_Parties_.pdf
1: 1569811575.pdf --> (QHUJ\_2SWLPL]DWLRQ_7KURXJK_7UDI¿F_$JJUHJDWLRQ_LQ_:LUHOHVV_1HWZRUNV_.pdf
1: 1569811661.pdf --> What_Scale_of_Audience_a_Campaign_can_Reach_in_What_Price_on_Twitter?_.pdf
3: 1569811665.pdf
1: 1569811675.pdf --> Coverage_in_Visual_Sensor_Networks_with_Pan-Tilt-Zoom_Cameras:_the_MaxFoV_Problem_.pdf
1: 1569811689.pdf --> Communication_Through_Collisions:_Opportunistic_Utilization_of_Past_Receptions_.pdf
2: 1569811709.pdf --> —Physical_layer_cooperation_of_a_source_with_a_relay_.pdf
1: 1569811737.pdf --> Stochastic_Information_Management_for_Voltage_Regulation_in_Smart_Distribution_Systems_.pdf
1: 1569811753.pdf --> Assessment_of_Multi-Hop_Interpersonal_Trust_in_Social_Networks_by_Three-Valued_Subjective_Logic_.pdf
1: 1569811761.pdf --> Optimal_Delay_Bound_for_Maximum_Weight_Scheduling_Policy_in_Wireless_Networks_.pdf
3: 1569811771.pdf
1: 1569811811.pdf --> Exploiting_Mobility_in_Proportional_Fair_Cellular_Scheduling:_Measurements_and_Algorithms_.pdf
1: 1569811835.pdf --> Security_Vulnerability_and_Countermeasures_of_Frequency_Offset_Correction_in_802.11a_Systems_.pdf
1: 1569811839.pdf --> On_Multihop_Communications_For_In-Vehicle_Internet_Access_Based_On_a_TDMA_MAC_Protocol_.pdf
1: 1569811857.pdf --> FluidRating:_A_Time-Evolving_Rating_Scheme_in_Trust-based_Recommendation_Systems_Using_Fluid_Dynamics_.pdf
1: 1569811867.pdf --> Deep_Packet_Inspection_with_DFA-trees_and_Parametrized_Language_Overapproximation_.pdf
1: 1569811891.pdf --> On_the_Design_and_Analysis_of_Data_Center_Network_Architectures_for_Interconnecting_Dual-Port_Servers_.pdf
2: 1569811925.pdf --> 2014_IEEE_—Combined_Heat_and_Power_(CHP)_systems_are_well_—Combined_Heat_and_Power,_Lyapunov_Optimiza-_.pdf
1: 1569811969.pdf --> Price_of_Anarchy_in_Network_Routing_with_Class_based_capacity_Guarantees_.pdf
2: 1569811981.pdf --> GeoMob:_A_Mobility-aware_Geocast_Scheme_in_Metropolitans_via_Taxicabs_and_Buses_.pdf
1: 1569811993.pdf --> TideWatch:_Fingerprinting_the_Cyclicality_of_Big_Data_Workloads_.pdf
1: 1569812027.pdf --> A_New_Efficient_Physical_Layer_OFDM_Encryption_Scheme_.pdf
1: 1569812071.pdf --> Secure_Cloud_Storage_Meets_with_Secure_Network_Coding_.pdf
1: 1569812087.pdf --> Unleashing_Exposed_Terminals_in_Enterprise_WLANs:_A_Rate_Adaptation_Approach_.pdf
1: 1569812089.pdf --> Throughput-Efficient_Channel_Allocation_in_Multi-Channel_Cognitive_Vehicular_Networks_.pdf
1: 1569812185.pdf --> Physical_Layer_Challenge-Response_Authentication_in_Wireless_Networks_with_Relay_.pdf
1: 1569812585.pdf --> FastProbe:_Malicious_User_Detection_in_Cognitive_Radio_Networks_Through_Active_Transmissions_.pdf
1: 1569812593.pdf --> User_Mobility_from_the_View_of_Cellular_Data_Networks_.pdf


```
