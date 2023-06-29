.. figure:: _static/eidalogo.jpg

Usage Examples
==============

Webservices are the easiest way to download data from ORFEUS EIDA and requests are resolved from URLs that return data. They can be invoked by your browser, a command line tool, or automatically through software package like `ObsPy <https://docs.obspy.org/packages/obspy.clients.fdsn.html#module-obspy.clients.fdsn>`_ and `fdsnws_fetch <https://www.seiscomp3.org/wiki/doc/applications/fdsnws_fetch>`_. Data can be requested by querying the webservice with a standardized syntax. Each call consists of the webservice address followed by a service label and finalized by one or more option-value pairs that represent the request options that are initialized by a question mark.

``https://webservice-address/label?option=value&option2=value2``

I want to download raw waveform data (FDSN Dataselect)
******************************************************

FDSNWS-Dataselect must be used to download waveform data. This example requests raw waveform data between 2014-01-01T00:20:00 and 2014-01-01T00:50:00 for station FR.RENF from EIDA node RESIF. The response will be a single mSEED file that contains all streams that fit this request. The output streams are limited to the contacted nodes' data holdings.

``https://ws.resif.fr/fdsnws/dataselect/1/query?starttime=2014-01-01T00:20:00&endtime=2014-01-01T00:50:00&network=FR&station=RENF``

Stations that belong to other networks may need to be downloaded from another data center. Alternatively, data can be downloaded using the EIDAWS-Federator web service. In this case user does not need to know which data center holds the desired waveforms.

``https://federator.orfeus-eu.org/fdsnws/dataselect/1/query?starttime=2014-01-01T00:20:00&endtime=2014-01-01T00:50:00&network=FR&station=RENF``


I want station metadata & instrument specifics (FDSN Station)
*************************************************************

Station metadata can be retrieved using FDSNWS-Station. This example requests station metadata from EIDA node NOA for stations within 0.7° arc-distance of 40°N, 23°E. The response will be a stationXML file with stations located in the selected area. Note that this request will only return stations within the data holdings of the respective node.

``https://eida.gein.noa.gr/fdsnws/station/1/query?latitude=40&longitude=23&maxradius=0.7``

Alternatively, station metadata and instrument response can be requested for stations or networks.

``https://www.orfeus-eu.org/fdsnws/station/1/query?network=NL&station=HGN&level=response``

Stations that belong to other networks may need to be downloaded from another data center. The EIDAWS-Federator web service can be used to browse entire EIDA metadata inventory in a single request. Following request will return metadata of stations located within 5° arc-distance of 42.645°N, 18.016°E (Dubrovnik) hosted by INGV, NOA and NIEP.

``https://federator.orfeus-eu.org/fdsnws/station/1/query?latitude=42.645&longitude=18.016&maxradius=5``

I want to know what data is available (FDSNWS Availability)
***********************************************************

Use FDNSWS-Availability to obtain information on what time segments are available for the archives. The following request will show you the coverage for which data is available for station FR.RENF from RESIF.

``https://ws.resif.fr/fdsnws/availability/1/query?starttime=2014-01-01T00:20:00&endtime=2014-02-01T00:00:00&network=FR&station=RENF``

I want to know what data center to download from (EIDA Routing)
***************************************************************

Use EIDAWS-Routing when unsure about what EIDA node holds the networks or stations you are interested in. Requesting dataselect (i.e. raw waveform data) routing information for network GE. The response is a JSON file that tells you this particular network belongs to GFZ and the waveform data can be retrieved from the returned webservice URL.

``https://orfeus-eu.org/eidaws/routing/1/query?network=GE&service=dataselect``

I want waveform metadata & quality metrics (EIDA WFCatalog)
***********************************************************

The EIDAWS-WFCatalog holds information on waveform metadata. This example requests waveform metadata from ODC between 2014-06-01 and 2014-06-03 for station NL.HGN excluding all streams with gaps. The response is a JSON file containing metadata documents for daily streams that pass the gapless criteria.

``https://www.orfeus-eu.org/eidaws/wfcatalog/alpha/query?start=2014-06-01&end=2014-06-03&network=NL&sta=HGN&num_gaps=0``
