<template>
  <div class="list">

    <!-- lets display the data -->
    <table class="table">
      <thead>
        <tr>
          <th scope="col">Symbol</th>
          <th scope="col">Name</th>
          <th scope="col">Price</th>
          <th scope="col">Sector</th>
          <th scope="col">52 Week High</th>
          <th scope="col">52 Week Low</th>
          <th scope="col">Dividend Yield</th>
          <th scope="col">EBITDA</th>
          <th scope="col">Earnings/Share</th>
          <th scope="col">Market Cap</th>
          <th scope="col">Price/Book</th>
          <th scope="col">Price/Earnings</th>
          <th scope="col">Price/Sales</th>
          <th scope="col">SEC Filings</th>        

        </tr>
      </thead>

      <tbody>
        <tr v-for="company in companies" :key="company.Symbol">
          <td>{{ company.Symbol }}</td>
          <td>{{ company.Name }}</td>
          <td>{{ company.Price }}</td>
          <td>{{ company.Sector }}</td>
          <td>{{ company['52 Week High'] }}</td>
          <td>{{ company['52 Week Low'] }}</td>
          <td>{{ company['Dividend Yield'] }}</td>
          <td>{{ company.EBITDA }}</td>
          <td>{{ company['Earnings/Share'] }}</td>
          <td>{{ company['Market Cap'] }}</td>
          <td>{{ company['Price/Book'] }}</td>
          <td>{{ company['Price/Earnings'] }}</td>
          <td>{{ company['Price/Sales'] }}</td>
          <td><a :href="company['SEC Filings']">More info...</a></td>
          
        </tr>
      </tbody>
    </table>
    
  </div>
</template>

<script>
export default {
  name: 'ListOfCompanies',
  props: {
    companies: Array
  }
}
</script>

<style scoped>

</style>
