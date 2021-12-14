<template>
  <div class="grid md:grid-cols-2 gap-4">

    <!-- Box 1 -->
      <div class="shadow-md bg-blue-100 p-10 text-center rounded">
          <h3 class="text-3xl text-blue-900 font-bold mb-4">Cases</h3>

            <div class="text-2xl mb-4">
                <span class="font-bold">New:</span>
                {{ numberComma(stats.NewConfirmed) }}
            </div>
            <div class="text-2xl mb-4">
                <span class="font-bold">Total:</span>
                {{ numberComma(stats.TotalConfirmed) }}
            </div>
      </div>
      <!-- End of Box 1 -->
      <!-- Box 2 -->
      <div class="shadow-md bg-blue-200 p-10 text-center rounded">
          <h3 class="text-3xl text-blue-900 font-bold mb-4">Deaths</h3>

            <div class="text-2xl mb-4">
                <span class="font-bold">New:</span>
                {{ numberComma(stats.NewDeaths) }}
            </div>
            <div class="text-2xl mb-4">
                <span class="font-bold">Total:</span>
                {{ numberComma(stats.TotalDeaths) }}
            </div>
      </div>
      <!-- End of Box 2 -->
  </div>
</template>

<script>
export default {
    name: 'DataBox',
    props: ['stats'],
    methods:{
        numberComma(x){
            return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
        }
    }
}
</script>

