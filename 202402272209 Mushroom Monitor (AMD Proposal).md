#Startup #Mushroom #Farming
**Automated Mushroom Harvest**

Vision Based Harvest Detection for Mushroom Farming

**What problem are you going to solve?**

We are automating the harvest process for mid-size mushroom farms. 
  

**What are you going to build to solve this problem? How is it different from existing solutions? Why is it useful?** 

We will build an automated system that automates yields by detecting when it is time to harvest, minimizing the time needed for human interaction in mushroom farming. Robotics in agriculture is not new, but mushroom are uniquely suited to automation. Mushrooms do not need light to grow, have predictable growth rates, and grow on substrate that is often the waste from other processes. Demand for mushrooms, both gourmet and medicinal, rose at a rate of 9.7% in 2023. However, most commercial mushroom farms are completely reliant on a the knowledge and experience of the farmers, with very little automation. 

The challenges of mushroom growing can be addressed with automation. Many gourmet mushrooms have a very short window of freshness, during which they must be picked. This means the farm must be monitored 24/7, by a person in order to maximize yield. This means the farmer must walk through the grow area, risking spore inhalation, contamination, and poor temperature control from the hourly door opening. 

Our system minimizes contact, and maintains optimal growth parameters for mushrooms. Some control systems on the market exist to control humidity and temperature, but none leverage the advancements in computer vision to detect pick times. Extremely large scale growers will use climate controlled warehouses, but sterilization becomes an issue. Contamination is a common cause of mushroom failure, and appears as distinct patches of color on the surface of the fruiting body. In the future, we envision a complete system that will selectively kill contamination, and increase yields. 



**How does your solution work? What are the main features? Please specify how you will use the AMD AI Hardware in your solution.**

This project is one step towards a completely robotic mushroom farm, but is scoped to be realistic given the time frame. Utilizing the AMD Kria KR260 Robotics Kit, paired with either its native camera modules or cost-effective USB cameras, we propose a system that adapts a machine learning model for mushroom detection and harvest prediction, inspired by AMD's Defect Detection Accelerated Application

Cameras will be set up in front of fruiting mycelial blocks and take periodic photos. These photos are fed into the ML system that analyzes the fruiting block for size of fruit and signs of surface contamination. If a fruit is ready, the system will send an notification to a web interface.

This project requires a custom machine learning classifier. There are a number of agricultural data sets, but none that focus on mushrooms. We believe we will be able to use the DeepFruits dataset in conjunction with our own data to fine-tune a classification model for the most common format of growing (mycelial bags). We also focus on Pink Oysters, which have a very distinct fruiting body and have many visual similarities to traditional fruit. The Kira will allow us to deploy our system quickly, leverage existing models, run directly on the DPU. 


Hardware
USB Camera or Native Camera Module
AMD Kria KR260 Robotics Kit

Software
TensorFlow for model training
OpenCV for image detection. 
Dataset of mushroom growth phases collected from online, my personal mushroom farm, and local growers. 
Python (Flask) for web application. 




  

The manipulation portion of the harvest problem will not be addressed due to hardware limitations.#Startup #Mushroom