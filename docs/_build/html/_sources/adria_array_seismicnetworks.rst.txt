AdriaArray - Seismic networks
====================

In various stages of planning and for different purposes, we prepared maps showing the distribution of permanent stations and suggested locations of temporary stations. The maps cover a range of complexity from very simple ones using just two colors to more comples figures explaining the station distribution in detail. Below, we show some of maps. All the maps and supporting files can be downloaded from the `AdriaArray GitHub repository <https://github.com/PetrColinSky/AdriaArray>`_.


AdriaArray Github repository
-------------------------------

The repository contains the `AdA folder <https://github.com/PetrColinSky/AdriaArray/tree/master/AdA>`_, which includes `permanent <https://github.com/PetrColinSky/AdriaArray/blob/master/AdA/InventoryPermanent.xls?raw=true>`_ and `temporary <https://github.com/PetrColinSky/AdriaArray/blob/master/AdA/InventoryTemporary.xls?raw=true>`_ station inventories.

The following two texts files describe what else you can find in the AdriaArray Github repository.

The file `maps-legend.pdf <https://github.com/PetrColinSky/AdriaArray/blob/master/AdA/maps-legend.pdf?raw=true>`_ explains how the AdriaArray network was planned and what can be seen on the maps. It is enough to read this text to understand the maps provided.

The file `maps-manual.pdf <https://github.com/PetrColinSky/AdriaArray/blob/master/AdA/maps-manual.pdf?raw=true>`_ talks about the scripts and how to produce the maps from the station inventories. This could be useful when you are about to modify the scripts and produce your own maps.

If you want to just take the maps provided, go to `AdA/MAPS/ <https://github.com/PetrColinSky/AdriaArray/tree/master/AdA/MAPS>`_.

If you want to display the stations in GoogleEarth, go to `AdA/GOOG/ <https://github.com/PetrColinSky/AdriaArray/tree/master/AdA/GOOG>`_ to get the .kml files. 

The folder `presentations <https://github.com/PetrColinSky/AdriaArray/tree/master/presentations>`_ contains some of the slides and poster about the AdriaArray Seismic Network presented in last years.

Stations maps
-----------------------------

.. image:: https://raw.githubusercontent.com/PetrColinSky/AdriaArray/master/AdA/MAPS/06AdriaBBovr.png
   :width: 600
   
Highly simplified map showing only the permanent and mobile stations regardless of their type.

.. image:: https://raw.githubusercontent.com/PetrColinSky/AdriaArray/master/AdA/MAPS/01AdriaTotal.png
   :width: 600
   

Permanent stations, both inside and outside of the AdA region, grouped by the corner period into 3 categories (red: corner period of 60 s and longer, orange: corner period between = 40 and < 60 s, yellow: corner period = 30 s).
Dark blue are the PACASE stations planned to stay in place for the AdriaArray. Light green are the stations which were agreed by the local network operators as a suitable spots for deployment of mobile BB station. These include short-period stations, accelerometers and BB stations with corner period < 30 s.
Light blue are the spots where there was a station before, so called “unequipped spots”.
White is the same category as green, but for these, we did not asked to serve as a places for mobile upgrade as these spots were not needed for the backbone. Gray are the stations not available or suitable for upgrade.
Dark green are BB stations to be build in near future of 1 year.
Five different pinkish colors show the mobile stations for respective subgroups. These triangles are empty inside. This allows to see that sometimes there is a permanent spot under. It means, such a mobile station is suggested to be placed at existing spot.
These are light blue (unequipped spots), green (< 30 s, SP/SM stations) as well as yellow (= 30 s stations).

Station names: For permanent stations, their respective names are shown in the map.
For mobile stations, several situations can happen: if the mobile is suggested to be placed at the permanent spot, again the permanent name is shown. If it is a PACASE spot, the given PACASE temporary name is used. If it is a former AlpArray spot, the given temporary AlpArray name is used. If it is an unequipped spot where there was a name found for that spot, this name is used (e.g. CASE stations), sometimes simply the name of the village is shown.
In Romania, these places are named as ZROxx, where xx is a number. When the mobile station is suggested at a new place, which needs to be scouted for, the name is created using two characters showing the country of deployment plus two digits with a numbering in the respective country.

Permanent stations outside of the AdriaArray region are shown by empty triangles with respective color as in the legend.
Big white and blue ellipses show schematically the planned local experiments.
The station colors of this map are reflected in the `.kml files <https://github.com/PetrColinSky/AdriaArray/tree/master/AdA/GOOG>`_, and hence one can reproduce almost the same layout also in GoogleEarth. In the `01AdriaTotal <https://raw.githubusercontent.com/PetrColinSky/AdriaArray/master/AdA/MAPS/01AdriaTotal.png>`_ map, all stations with corner period of 60 s and longer are shown by red triangles. The .kml files have additional two bands corresponding to the map `17AdAcorners <https://raw.githubusercontent.com/PetrColinSky/AdriaArray/master/AdA/MAPS/17AdAcorners.png>`_, see below.

.. image:: https://raw.githubusercontent.com/PetrColinSky/AdriaArray/master/AdA/MAPS/17AdAcorners.png
   :width: 600

Map shows both permanent and temporary stations (backbone) split by five corner period ranges. Note, that in the previous maps, the red color denoted all corner periods of 60 s and longer, while here, red is used for 60 s up to 120 s only. Longer corner periods have then additional colors for 120 – 240 s range and for 240 and longer.
   

Stations list
-----------------------------
The data and metadata of all permanent and temporary stations belonging to the AdriaArray Seismic Network are availalbe via EIDA. The temporary networks are registered and listed by `FDSN <https://www.fdsn.org/networks/?search=adriaarray>`_.

Broadband stations covering homogeneously the AdriaArray region outlined by the yellow line in the maps form the AdriaArray backbone. The shortest corner period of the backbone is 30s. To download the data, a virtual network _ADARRAY can be used. All broadband stations in the region with HH* and BH* channels are included in _ADARRAY. According to the SEED convention, H** and B** channels are assigned for sensors with corner period of equal or longer than 10 s. _ADARRAY virtual network hence includes more stations than the AdriaArray backbone. The backbone is a subset of _ADARRAY.


Network & station availability
--------------------------------

Current status of the deployment of mobile stations:

.. image:: https://raw.githubusercontent.com/PetrColinSky/AdriaArray/master/AdA/MAPS/13AdriaDploy.png
   :width: 600   


Relation between EIDA nodes and network codes:

.. image:: https://raw.githubusercontent.com/PetrColinSky/AdriaArray/master/AdA/MAPS/16AdAnetwork.png
   :width: 600   



AdriaArray - Local experiments
--------------------------------

Representatives of each Arria Array members will be contacted shortly to provide us more information regarding the current status of local seismic deployments.
This section will be updated accordingly.

	- Experiment 1
Description
   
	- Experiment 2
Description
   
	- Experiment 3
Description
   
	- Experiment 4
Description
   
	- Experiment 5
Description

AdriaArray - Data availability
-------------------------------

How to access the data?
-----------------------------
	- The seismic embargoed data will be available to the participants `through EIDA nodes <https://www.orfeus-eu.org/data/eida/webservices/station/>`_.


How to cite the data?
-----------------------------
	- For each network code belonging to the AdriaArray initiative, `a DOI <https://www.fdsn.org/networks/?search=adriaarray>`_ will be registered, allowing to cite the data.




.. _adria_array_seismicnetworks: 

