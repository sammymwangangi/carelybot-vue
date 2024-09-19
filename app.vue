<template>
  <div class="flex h-screen flex-col bg-gray-100">
    <!-- Header -->
    <header class="bg-white shadow-sm">
      <div class="mx-auto max-w-7xl px-4 py-4 sm:px-6 lg:px-8">
        <h1 class="text-2xl font-semibold text-gray-900">
          Carelybot Dashboard
        </h1>
      </div>
    </header>
    <!-- Main Section -->
    <main class="flex-1 overflow-hidden p-4 sm:p-6 lg:p-8">
      <ScrollArea class="h-full">
        <div class="grid gap-6 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4">
          <Card
            v-for="(patient, index) in patients"
            :key="index"
            class="overflow-hidden transition-all duration-300 hover:shadow-lg hover:-translate-y-1"
          >
            <CardContent class="p-6 bg-gradient-to-br from-white to-gray-50">
              <div class="mb-4 flex items-center justify-between">
                <!-- Patient Name -->
                <h2 class="text-xl font-bold text-gray-800 tracking-tight">
                  {{ patient.name }}
                </h2>
                <!-- Patient Health Status -->
                <Badge
                  :variant="
                    patient.status === 'STABLE' ? 'secondary' : 'destructive'
                  "
                  class="text-xs font-semibold px-2 py-1"
                >
                  {{ patient.status }}
                </Badge>
              </div>
              <!-- Patient Room Number -->
              <div class="mb-6 flex items-center text-sm text-gray-600">
                <BedDouble class="mr-2 h-4 w-4" /> {{ patient.roomNumber }}
              </div>
              <div class="grid grid-cols-3 gap-4 text-center mb-6">
                <!-- Heart Rate -->
                <div
                  class="flex flex-col items-center bg-red-50 rounded-lg p-2"
                >
                  <Heart class="mb-2 h-6 w-6 text-red-500" />
                  <span class="text-lg font-semibold text-gray-800">{{
                    patient.heartRate
                  }}</span>
                  <span class="text-xs text-gray-500">BPM</span>
                </div>
                <!-- Breath Rate -->
                <div
                  class="flex flex-col items-center bg-blue-50 rounded-lg p-2"
                >
                  <Wind class="mb-2 h-6 w-6 text-blue-500" />
                  <span class="text-lg font-semibold text-gray-800">{{
                    patient.breathRate
                  }}</span>
                  <span class="text-xs text-gray-500">BPM</span>
                </div>
                <!-- Last Measurement -->
                <div
                  class="flex flex-col items-center bg-green-50 rounded-lg p-2"
                >
                  <Activity class="mb-2 h-6 w-6 text-green-500" />
                  <span class="text-sm font-medium text-gray-800">{{
                    patient.lastMeasurement
                  }}</span>
                  <span class="text-xs text-gray-500">Last</span>
                </div>
              </div>
              <!-- Check if there is alert -->
              <div
                v-if="patient.alertCount > 0"
                class="mt-4 flex items-center justify-center text-red-600 bg-red-50 rounded-full py-2"
              >
                <AlertCircle class="mr-2 h-5 w-5" />
                <span class="text-sm font-semibold">
                  {{ patient.alertCount }} Alert{{
                    patient.alertCount > 1 ? "s" : ""
                  }}
                </span>
              </div>
            </CardContent>
          </Card>
        </div>
      </ScrollArea>
    </main>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { Badge } from "@/components/ui/badge";
import { Card, CardContent } from "@/components/ui/card";
import { ScrollArea } from "@/components/ui/scroll-area";
import { BedDouble, Heart, Wind, Activity, AlertCircle } from "lucide-vue-next";

// Data
const patients = ref([
  {
    name: "Anatolij Abramovič",
    roomNumber: "SA231",
    status: "STABLE",
    heartRate: 75,
    breathRate: 16,
    lastMeasurement: "3:45 AM",
    alertCount: 0,
  },
  {
    name: "Vardas -",
    roomNumber: "D04",
    status: "CRITICAL",
    heartRate: 120,
    breathRate: 22,
    lastMeasurement: "2:52 PM",
    alertCount: 1,
  },
  {
    name: "Petras Simenas",
    roomNumber: "D02",
    status: "CRITICAL",
    heartRate: 110,
    breathRate: 20,
    lastMeasurement: "4:36 PM",
    alertCount: 1,
  },
  {
    name: "Vladas Pavardenis",
    roomNumber: "D01",
    status: "CRITICAL",
    heartRate: 115,
    breathRate: 21,
    lastMeasurement: "11:09 PM",
    alertCount: 1,
  },
  {
    name: "Ignacas Adolis Gulbinas",
    roomNumber: "SA209",
    status: "CRITICAL",
    heartRate: 105,
    breathRate: 19,
    lastMeasurement: "11:22 AM",
    alertCount: 1,
  },
]);
</script>

<style scoped>
/* custom styles here */
</style>
