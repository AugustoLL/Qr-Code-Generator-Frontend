<template>
  <v-container class="fill-height">
    <v-responsive
      class="align-centerfill-height mx-auto"
      max-width="1200"
    >

      <div class="text-center">
        <h1 class="text-h2 font-weight-bold">QR Code Generator</h1>
      </div>

      <div class="py-4"></div>

      <v-row>
        <v-col :cols="mobile ? 12 : 6">
          <v-card
            class="py-4"
            color="secondary"
            rounded="lg"
            variant="outlined"
          >
          <v-card-title>Let's make a QR Code!</v-card-title>
          <v-card-subtitle>Complete the following form:</v-card-subtitle>
            <v-form v-model="isFormValid" @submit.prevent="generateQRCode">
              <v-container>
                <v-row>
                  <!-- <input type="url" name="url" id="url" v-model="url.value"> -->
                  <v-text-field
                    class="mb-2 mx-4"
                    prepend-icon="mdi-link-variant"
                    label="URL"
                    v-model="url.value.value"
                    :rules="url.rules"
                    hide-details="auto"
                    type="url"
                  ></v-text-field>
                </v-row>
                <v-row>
                  <v-icon icon="mdi-image-multiple"></v-icon>
                  <v-card-title>Format</v-card-title>
                  <v-chip-group
                    class="mb-2 mx-4"
                    label="Format"
                    v-model="format.value.value"
                    :rules="format.rules"
                    hide-details="auto"
                    mandatory
                  >
                  <v-chip 
                    v-for="format in validFormats"
                    :key="format"
                    :text="format"
                    :value="format"
                    variant="outlined" 
                    filter
                  ></v-chip>
                </v-chip-group>
                </v-row>
                <v-row>
                  <v-text-field
                    class="mb-2 mx-4"
                    prepend-icon="mdi-ruler"
                    label="Size"
                    v-model="size.value.value"
                    :rules="size.rules"
                    hide-details="auto"
                    type="number"
                  ></v-text-field>
                </v-row>
                <v-row>
                  <v-color-picker 
                  class="mb-2 mx-4"
                    v-model="patternColor.value.value" 
                    mode="hex" 
                    :modes="['hex']"
                    rounded="lg"
                    :width="mobile ? '100%' : '40%'"
                  ></v-color-picker>
                  <v-color-picker 
                    class="mb-2 mx-4"
                    v-model="backgroundColor.value.value" 
                    mode="hex" 
                    :modes="['hex']"
                    rounded="lg"
                    :width="mobile ? '100%' : '40%'"
                  ></v-color-picker>
                </v-row>
                <v-row>
                  <v-text-field
                    class="mb-2 mx-4"
                    prepend-icon="mdi-image-filter-tilt-shift"
                    label="Logo URL"
                    v-model="logoUrl.value.value"
                    :rules="logoUrl.rules"
                    hide-details="auto"
                    type="url"
                  ></v-text-field>
                </v-row>
                <v-row>
                  <v-btn type="submit" :disabled="!isFormValid" variant="outlined" color="primary" class="mt-4">
                    Generate
                  </v-btn>
                </v-row>
              </v-container>
            </v-form>
          </v-card>
        </v-col>

        <v-col :cols="mobile ? 12 : 6">
          <v-card
            class="py-4 px-4"
            color="primary"
            rounded="lg"
            variant="outlined"
          >
            <v-img
            v-if="qrCodeImage"
            :src="qrCodeImage"
            alt="QR Code"
            rounded="lg"
            position="center"
            >
              <template v-slot:placeholder>
                <div class="d-flex align-center justify-center fill-height">
                  <v-progress-circular
                    color="primary"
                    indeterminate
                  ></v-progress-circular>
                </div>
              </template>
            </v-img>

            <h2>{{ error }}</h2>

            <template #title>
              <h2 class="text-h5 font-weight-bold">Preview</h2>
            </template>

            <template #subtitle>
              <div class="text-subtitle-1">
              </div>
            </template>
          </v-card>
        </v-col>
      </v-row>
    </v-responsive>
  </v-container>
</template>

<script setup lang="ts">
  import { ref, watch, computed } from 'vue';
  import { useDisplay } from 'vuetify';
  import axios from 'axios';

  const { mobile } = useDisplay();

  let error = '';
  const qrCodeImage = ref('');
  const isFormValid = ref(false);
  const url = {
    value: ref(''),
    formatted: computed(() : string => {
      if (!url.value.value.startsWith('http://') && !url.value.value.startsWith('https://')) {
        return `https://${url.value.value}`;
      }
      return url.value.value;
    }),
    rules: [
      (value: string) => typeof value === 'string' || 'Must be a string',
      (value: string) => !!value || 'This field is required.',
      (value: string) => value.length <= 2000 || 'Max 2000 characters',
      (value: string) => {
        const pattern = /^https?:\/\/(?:www\.)?[-a-zA-Z0-9@:%._\+~#=]{1,256}\.[a-zA-Z0-9()]{1,6}\b(?:[-a-zA-Z0-9()@:%_\+.~#?&\/=]*)$/;
        return pattern.test(value) || 'Invalid URL. Example: https://example.com'
      },
    ],
  };
  const validFormats = ['png', 'jpg', 'jpeg'];
  const format = {
    value: ref('png'),
    rules: [
      (value: string) => !!value || 'This field is required.',
      (value: string) => ('png' || 'jpg' || 'jpeg') === value || 'Invalid format.',
    ],
  };
  const size = {
    value: ref(500),
    rules: [
      // (value: number) => typeof value === 'number' || 'Must be a number.',
      (value: number) => !!value || 'This field is required.',
      (value: number) => value >= 100 || 'Min 100px',
      (value: number) => value <= 1080 || 'Max 1080',
    ],
  };
  const patternColor = {
    value: ref('#000000'),
    rules: [
      (value: string) => !!value || 'This field is required.',
    ],
  };
  const backgroundColor = {
    value: ref('#ffffff'),
    rules: [
      (value: string) => !!value || 'This field is required.',
    ],
  };
  const logoUrl = {
    value: ref(''),
    rules: [
      (value: string) => value.startsWith('http://') || value.startsWith('https://') || 'Invalid URL.',
      (value: string) => value.length <= 2000 || 'Max 2000 characters',
      (value: string) => {
        const pattern = /^https?:\/\/(?:www\.)?[-a-zA-Z0-9@:%._\+~#=]{1,256}\.[a-zA-Z0-9()]{1,6}\b(?:[-a-zA-Z0-9()@:%_\+.~#?&\/=]*)$/;
        return pattern.test(value) || 'Invalid URL. Example: https://example.com'
      },
    ],
  };
  const generateQRCode = async () => {
    const params = new URLSearchParams({
      url: url.formatted.value,
      format: format.value.value,
      size: size.value.value.toString(),
      darkColor: patternColor.value.value,
      lightColor: backgroundColor.value.value,
      logoUrl: logoUrl.value.value,
    });

    try {
      const response = await axios.get(`http://localhost:8080/api/generate?${params}`, { responseType: 'arraybuffer' });

      const base64String = btoa(
        new Uint8Array( await response.data).reduce(
          (data, byte) => data + String.fromCharCode(byte),
          ''
        )
      );

      qrCodeImage.value = `data:image/${format.value.value};base64,${base64String}`;
    } catch (error) {
      console.error(error);
      qrCodeImage.value = '';
      error = 'An error occurred while generating the QR code.'
    }
  };

  watch([url.value, format.value, size.value, qrCodeImage.value], () => { 
    if (isFormValid.value) generateQRCode();
  });
</script>
