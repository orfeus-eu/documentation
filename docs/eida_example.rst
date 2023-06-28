.. figure:: _static/eidalogo.jpg

Usage Examples
==============

Webservices are the easiest way to download data from ORFEUS EIDA and requests are resolved from URLs that return data. They can be invoked by your browser, a command line tool, or automatically through software package like `ObsPy <https://docs.obspy.org/packages/obspy.clients.fdsn.html#module-obspy.clients.fdsn>`_ and `fdsnws_fetch <https://www.seiscomp3.org/wiki/doc/applications/fdsnws_fetch>`_. Data can be requested by querying the webservice with a standardized syntax. Each call consists of the webservice address followed by a service label and finalized by one or more option-value pairs that represent the request options that are initialized by a question mark.

``https://webservice-address/label?option=value&option2=value2``

.. dropdown:: I want to download raw waveform data (FDSN Dataselect)

    FDSNWS-Dataselect must be used to download waveform data. This example requests raw waveform data between 2014-01-01T00:20:00 and 2014-01-01T00:50:00 for station FR.RENF from EIDA node RESIF. The response will be a single mSEED file that contains all streams that fit this request. The output streams are limited to the contacted nodes' data holdings.

    ``https://ws.resif.fr/fdsnws/dataselect/1/query?starttime=2014-01-01T00:20:00&endtime=2014-01-01T00:50:00&network=FR&station=RENF``

    Stations that belong to other networks may need to be downloaded from another data center. Alternatively, data can be downloaded using the EIDAWS-Federator web service. In this case user does not need to know which data center holds the desired waveforms.

    ``https://federator.orfeus-eu.org/fdsnws/dataselect/1/query?starttime=2014-01-01T00:20:00&endtime=2014-01-01T00:50:00&network=FR&station=RENF``

