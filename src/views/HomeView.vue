<template>
    <div class="max-w-screen-sm mx-auto px-4 py-10">
        <router-link :to="{name: 'Personal'}">
            <div class="max-w-md mx-auto bg-white rounded-md shadow-md overflow-hidden">
            <div class="p-4">
                <h2 class="text-xl font-semibold mb-2">New Client</h2>
                <p class="text-gray-600">Click to create a new client</p>
            </div>
        </div>
        </router-link>
        <router-link to="#">
            <div class="mt-8 max-w-md mx-auto bg-white rounded-md shadow-md overflow-hidden">
            <div class="p-4">
                <h2 class="text-xl font-semibold mb-2">Existing Client</h2>
                <p class="text-gray-600">Click to fill records for an existing client</p>
            </div> 
        </div>
        </router-link>
        

        
    </div>
</template>

<script>

</script>

<style></style>