<template>
	<button
    v-for="item in items"
    :key="item.id"
    type="button"
    @click="setMapCenter(item)"
  >
    изменить позицию {{item.title}}
  </button>
	<yandex-map
    :coordinates="coordinates"
    :detailed-controls="detailedControls"
    :controls="controls"
    @created="onMapCreated"
  >
    <yandex-marker
      v-for="item in items"
      :key="item.id"
      :marker-id="item.id"
      :coordinates="[item.lat, item.lon]"
    />
  </yandex-map>
  </template>
  
  <script setup>
  import { ref } from "vue"
  import { YandexMap, YandexMarker } from 'vue-yandex-maps';

  const items = [
        {
          id: 999,
          title: "Европочта, Отделение № 999",
          subtitle: "г.Минск, ул.Ангарская, 62А",
          lat: "53.87999999999999",
          lon: "27.683455306746517",
          rating: "4,6",
        },
        {
          id: 123,
          title: "Европочта, Отделение № 123",
          subtitle: "Минск, ул. Сурганова, 54",
          lat: "53.87222222222222",
          lon: "27.683455306746517",
          rating: "4,6",
        },
        {
          id: 156,
          title: "Европочта, Отделение № 6",
          subtitle: "Минск, ул. Притыцкого, 156",
          lat: "53.87660859946719",
          lon: "27.683455306746517",
          rating: "4,6",
        },
      ]
	  let mapObject = '';
      const coordinates = [53.87660859946719, 27.683455306746517];
      const controls = ["fullscreenControl"];
      const detailedControls = { zoomControl: { position: { right: 10, top: 50 } } }

	const onMapCreated = (map) => {
		mapObject = map;
	};
	
    const setMapCenter = (item) => {
		const coords = [item.lat, item.lon]
		mapObject.setCenter(coords, 17);
	};
	
  
  </script>
  
  <style>
  .yandex-container {
	height: 400px;
  }
  
  </style>