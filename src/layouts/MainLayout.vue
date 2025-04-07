<template>
  <q-layout view="hHh lpR fFf" class="layout-cinema">
    <!-- Header -->
    <q-header elevated class="bg-header text-white">
      <q-toolbar class="justify-between">
        <!-- Logo + Titel -->
        <div class="flex items-center">
          <q-btn flat round dense icon="movie" class="text-primary" @click="$router.push('/')" />
          <q-toolbar-title class="text-primary cursor-pointer text-weight-bold" @click="$router.push('/')">
            Movie Club
          </q-toolbar-title>
        </div>

        <!-- Suche -->
        <div class="search-container">
          <q-input
            v-model="search"
            dense
            standout
            clearable
            placeholder="Search..."
            color="primary"
            bg-color="white"
            class="search-input"
            style="border-radius: 10px; width: 300px;"
          >
            <template v-slot:append>
              <q-icon name="search" />
            </template>
          </q-input>
        </div>

        <!-- Benutzer Dropdown -->
        <div>
          <q-btn-dropdown
            flat
            round
            dense
            icon="account_circle"
            class="text-white"
            style="background-color: rgba(0, 188, 212, 0.2); border: 1px solid #00bcd4;"
            v-if="isAuthenticated !== null"
          >
            <q-list style="min-width: 160px">
              <q-item
                v-if="!isAuthenticated"
                clickable
                v-close-popup
                @click="loginUser"
              >
                <q-item-section avatar>
                  <q-icon name="login" class="text-primary" />
                </q-item-section>
                <q-item-section class="text-primary text-weight-bold">Login</q-item-section>
              </q-item>

              <template v-else>
                <q-item clickable v-close-popup @click="$router.push('/profile')">
                  <q-item-section avatar>
                    <q-icon name="account_box" class="text-primary" />
                  </q-item-section>
                  <q-item-section class="text-primary text-weight-bold">Profile</q-item-section>
                </q-item>
                <q-item clickable v-close-popup @click="logoutUser">
                  <q-item-section avatar>
                    <q-icon name="logout" class="text-primary" />
                  </q-item-section>
                  <q-item-section class="text-primary text-weight-bold">Logout</q-item-section>
                </q-item>
              </template>
            </q-list>
          </q-btn-dropdown>
        </div>
      </q-toolbar>
    </q-header>

    <!-- Seiteninhalt -->
    <q-page-container class="bg-page">
      <router-view />
    </q-page-container>

    <!-- Footer -->
    <q-footer class="bg-footer text-white q-pa-md text-center">
      <div>
        © 2025 Movie Club. All rights reserved.
      </div>
    </q-footer>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import { useAuth0 } from '@auth0/auth0-vue'

const search = ref('')
const { loginWithRedirect, logout, isAuthenticated } = useAuth0()

function loginUser() {
  loginWithRedirect()
}

function logoutUser() {
  logout({ returnTo: window.location.origin })
}
</script>

<style scoped>
.layout-cinema {
  background-color: #111;
  color: #fff;
}

.bg-header {
  background-color: #1c1c1c;
}

.bg-footer {
  background-color: #111;
  box-shadow: 0 -2px 8px rgba(0, 0, 0, 0.4);
}

.text-primary {
  color: #00bcd4 !important;
}

/* Suchfeld */
.search-input ::v-deep(.q-field__control) {
  background-color: rgba(255, 255, 255, 0.1);
  color: #00bcd4 !important;
  border: 1px solid #00bcd4 !important;
}

.search-input ::v-deep(.q-field__native),
.search-input ::v-deep(.q-placeholder) {
  color: #00bcd4 !important;
  opacity: 0.8;
}
</style>
