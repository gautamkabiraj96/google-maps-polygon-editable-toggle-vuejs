<template>
  <div>
    <div class="header-margins">
      Google Maps Polygon Editable Toggle
      <div class="np-credits">www.nightprogrammer.com</div>
    </div>
    <div class="np-toggle-btn" @click="togglePolygonEditable()">
      Toggle edit
    </div>
    <div id="polygon-editable-toggle" class="map-margins"></div>
  </div>
</template>

<script>
import loadGoogleMapsApi from "load-google-maps-api";
import { gMapsApiKey } from "./../constants";

export default {
  name: "EditablePolygonToggle",
  data() {
    return {
      map: null,
      polygonShape: null,
      polygonCoords: [
        { lat: 25.774, lng: -80.19 },
        { lat: 18.466, lng: -66.118 },
        { lat: 32.321, lng: -64.757 },
        { lat: 25.774, lng: -80.19 },
      ],
    };
  },
  methods: {
    togglePolygonEditable() {
      this.polygonShape.setEditable(!this.polygonShape.getEditable());
      this.polygonShape.setDraggable(!this.polygonShape.getDraggable());
    },
  },
  mounted() {
    loadGoogleMapsApi({
      key: gMapsApiKey,
      libraries: ["places", "drawing", "geometry"],
    }).then(async () => {
      const mapZoom = 12;
      const { google } = window;
      const mapOptions = {
        zoom: mapZoom,
        mapTypeId: google.maps.MapTypeId.HYBRID,
        center: new google.maps.LatLng({ lat: 23, lng: 57 }),
        mapTypeControl: true,
        streetViewControl: false,
        mapTypeControlOptions: {
          position: google.maps.ControlPosition.BOTTOM_LEFT,
        },
      };
      this.map = new google.maps.Map(
        document.getElementById("polygon-editable-toggle"),
        mapOptions
      );

      const tempBounds = new google.maps.LatLngBounds();

      for (let j = 0; j < this.polygonCoords.length; j++) {
        const x = {
          lat: this.polygonCoords[j].lat,
          lng: this.polygonCoords[j].lng,
        };
        const BoundLatLng = new google.maps.LatLng({
          lat: parseFloat(x.lat),
          lng: parseFloat(x.lng),
        });
        tempBounds.extend(BoundLatLng);
      }
      const centroid = tempBounds.getCenter();

      this.polygonShape = new google.maps.Polygon({
        paths: this.polygonCoords,
        strokeColor: "#f8fc03",
        map: this.map,
        strokeWeight: 3,
        fillColor: "#ff6f00",
        fillOpacity: 0.6,
        zIndex: 99999,
      });

      this.polygonShape.setMap(this.map);
      this.map.setCenter(centroid);
      this.map.setZoom(4);
    });
  },
};
</script>

<style scoped>
.header-margins {
  margin-left: 40px;
  margin-top: 20px;
}

.map-margins {
  height: 400px;
  width: 600px;
  margin: 30px 40px;
}
.np-toggle-btn {
  margin: 10px 40px;
  width: 120px;
  background: #eee;
  color: #000;
  text-align: center;
  border-radius: 4px;
  padding: 3px;
  cursor: pointer;
  transition: all 0.3s;
}
.np-toggle-btn:hover {
  margin: 10px 40px;
  width: 120px;
  background: rgb(0, 110, 255);
  color: #fff;
  text-align: center;
  border-radius: 4px;
  padding: 3px;
  cursor: pointer;
  transition: all 0.3s;
}
.np-credits {
  font-size: 12px;
}
</style>