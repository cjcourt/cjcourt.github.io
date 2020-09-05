
# Leaflet cluster map of talk locations

Run this from the _talks/ directory, which contains .md files of all your talks. This scrapes the location YAML field from each .md file, geolocates it with geopy/Nominatim, and uses the getorg library to output data, HTML, and Javascript for a standalone cluster map.


```python
!pip install getorg --upgrade
import glob
import getorg
from geopy import Nominatim
```

    Requirement already up-to-date: getorg in /home/vm/anaconda3/lib/python3.5/site-packages
    Requirement already up-to-date: geopy in /home/vm/.local/lib/python3.5/site-packages (from getorg)
    Requirement already up-to-date: retrying in /home/vm/.local/lib/python3.5/site-packages (from getorg)
    Requirement already up-to-date: pygithub in /home/vm/anaconda3/lib/python3.5/site-packages (from getorg)
    Requirement already up-to-date: six>=1.7.0 in /home/vm/.local/lib/python3.5/site-packages (from retrying->getorg)
    IPywidgets and ipyleaflet support enabled.



```python
g = glob.glob("*.md")
```


```python
geocoder = Nominatim()
location_dict = {}
location = ""
permalink = ""
title = ""
```


```python

for file in g:
    with open(file, 'r') as f:
        lines = f.read()
        if lines.find('location: "') > 1:
            loc_start = lines.find('location: "') + 11
            lines_trim = lines[loc_start:]
            loc_end = lines_trim.find('"')
            location = lines_trim[:loc_end]
                            
           
        location_dict[location] = geocoder.geocode(location)
        print(location, "\n", location_dict[location])

```

    Berkeley CA, USA 
     Berkeley, Alameda County, California, United States of America
    Los Angeles, CA 
     LA, Los Angeles County, California, United States of America
    London, UK 
     London, Greater London, England, UK
    San Francisco, California 
     SF, California, United States of America



```python
m = getorg.orgmap.create_map_obj()
getorg.orgmap.output_html_cluster_map(location_dict, folder_name="../talkmap", hashed_usernames=False)
```




    'Written map to ../talkmap/'




```python

```
