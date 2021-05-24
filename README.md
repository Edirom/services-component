# A web component for service monitors of ZenMEM and ViFE

The component's name is `services-component` and may be integrated in a website as follows:

```
<div>
    <services-component></services-component>
</div>
```

The data for the services should look like this:

```
{
    "create_datetime": 1621845012, 
    "monitors": [
        {
            "friendly_name": "service's friendly name", 
            "url": "https://service.url", "cluster": 
            "Cluster the service runs in", 
            "ip": "0.0.0.0", 
            "status": 2
        }, {
            "friendly_name": "service's friendly name ", 
            "url": "https://service.url", 
            "cluster": "Cluster the service runs in", 
            "ip": "0.0.0.0", 
            "status": 8
        }
    ]
}
```

Status codes may be:

* 0: service is paused
* 2: service is running
* 8 or 9: service is down

The data must be provided to the web component as follows:

```
<script>
    let xhttp = new XMLHttpRequest();

    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            let services = JSON.parse(this.responseText);
            const element = document.querySelector('services-component');
            element.services = services;
        }
    };
    xhttp.open('GET', 'https://services.zenmem.de/monitors.json', true);
    xhttp.send();
</script>
```