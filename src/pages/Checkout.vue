<template>
  <q-page>
    <div class="container row justify-center">
      <div>
        <p class="page-title jakarta-sb q-mb-none">Keranjang</p>
        <div class="divider q-mt-md" />
        <q-table :rows="rows" :columns="columns" row-key="name" class="table" grid hide-header hide-bottom>
          <template v-slot:item="props">
            <div class="column q-mt-md">
              <p class="store-text jakarta-sb q-mb-none q-mt-sm">{{ props.row.store }}</p>
              <p class="city-text jakarta-sb q-mb-none">{{ props.row.city }}</p>
            </div>
            <div class="cart-item row q-mt-sm q-mb-md">
              <q-icon :name="props.row.thumbnail" size="78px" />
              <div class="column justify-between q-ml-sm">
                <p class="name-text jakarta-sb q-mb-none">{{ props.row.name }}</p>
                <div v-if="props.row.discount > 0 || props.row < 100" class="row items-center q-mt-sm">
                  <div class="discount-bg">
                    <p class="discount-text jakarta-b q-mb-none q-pa-xs">{{ props.row.discount }}%</p>
                  </div>
                  <p class="discount-price-text jakarta-md q-mb-none q-ml-md">Rp <strike>{{ formatNumber(props.row.price)
                  }}</strike>
                  </p>
                  <p class="price-text jakarta-b q-mb-none q-mx-sm">Rp {{ formatNumber(calculateDiscount(props.row.price,
                    props.row.discount)) }}</p>
                </div>
                <p v-else class="price-text jakarta-b q-mb-none q-mt-sm">Rp {{ formatNumber(props.row.price) }}</p>
              </div>
            </div>
            <q-seperator class="divider" />
          </template>
        </q-table>
      </div>
      <q-card class="card q-py-md q-px-xl" flat>
        <p class="name-text jakarta-sb q-mb-none">Ringkasan Belanja</p>
        <div class="q-mt-md">
          <div class="row justify-between">
            <p class="summary-text q-mb-none">Total Harga</p>
            <p class="summary-text q-mb-none">{{ 'Rp ' + formatNumber(roughTotalCost) }}</p>
          </div>
          <div class="row justify-between">
            <p class="summary-text q-mb-none">Total Diskon Buah</p>
            <p class="summary-text q-mb-none">{{ '-Rp ' + formatNumber(totalDiscount) }}</p>
          </div>
        </div>
        <q-separator inset class="q-my-md" />
        <div class="row justify-between">
          <p class="total-cost-text q-mb-none">Ringkasan Belanja</p>
          <p class="total-cost-text q-mb-none">{{ 'Rp ' + formatNumber(totalCost) }}</p>
        </div>
        <q-btn class="buy-button jakarta-sb q-mt-lg" label="Beli" text-color="white" unelevated no-caps />
      </q-card>
    </div>
  </q-page>
</template>

<script>
const columns = [
  {
    name: 'name',
    required: true,
    label: 'Dessert (100g serving)',
    align: 'left',
    field: row => row.name,
    format: val => `${val}`,
    sortable: true
  },
  { name: 'calories', align: 'center', label: 'Calories', field: 'calories', sortable: true },
  { name: 'fat', label: 'Fat (g)', field: 'fat', sortable: true },
  { name: 'carbs', label: 'Carbs (g)', field: 'carbs' },
  { name: 'protein', label: 'Protein (g)', field: 'protein' },
  { name: 'sodium', label: 'Sodium (mg)', field: 'sodium' },
  { name: 'calcium', label: 'Calcium (%)', field: 'calcium', sortable: true },
  { name: 'iron', label: 'Iron (%)', field: 'iron', sortable: true }
]

const rows = [
  {
    name: 'Alpukat Mentega',
    store: 'Kebun Pak Ravi',
    thumbnail: 'img:icons/home/alpukat-mentega.png',
    price: 25200,
    discount: 10,
    city: 'Kabupaten Bojonegoro',
    rating: 5.0,
    sold: 500,
    kondisi: 'Baru panen',
    Berat: 3,
    desc: 'Lorem ipsum dolor sit amet, consectetur',
    stock: 20,
  },
  {
    name: 'Alpukat',
    store: 'Kebun Bu Salwa',
    thumbnail: 'img:icons/home/alpukat.png',
    price: 280000,
    city: 'Kota Kediri',
    rating: 5.0,
    sold: 81,
    kondisi: 'Baru panen',
    Berat: 3,
    desc: 'Lorem ipsum dolor sit amet, consectetur',
    stock: 20,
  },
]

export default {
  name: 'Checkout',

  setup() {
    return {
      columns,
      rows
    }
  },

  methods: {
    formatNumber(value) {
      return value.toLocaleString('en-US');
    },

    calculateDiscount(price, discount) {
      const discountAmount = price * (discount / 100);
      const discountedPrice = price - discountAmount;
      return discountedPrice;
    }
  },

  computed: {
    totalCost() {
      return this.rows.reduce((total, item) => {
        const price = item.discount > 0 ? this.calculateDiscount(item.price, item.discount) : item.price;
        return total + price;
      }, 0);
    },

    roughTotalCost() {
      return this.rows.reduce((total, item) => {
        return total + item.price;
      }, 0);
    },

    totalDiscount() {
      return this.rows.reduce((total, item) => {
        const discountAmount = item.discount > 0 ? item.price * (item.discount / 100) : 0;
        return total + discountAmount;
      }, 0);
    }
  }
}
</script>

<style>
.container {
  margin-top: 50px;
}

.table {
  width: 654px;
  height: min-content;
  margin-right: 125px;
}

.page-title {
  font-size: 24px;
  color: #323741;
}

.divider {
  width: 677px;
  height: 2px;
  background-color: #D9D9D9;
}

.cart-item {
  width: 654px;
  height: min-content;
}

.discount-bg {
  width: min-content;
  height: min-content;
  background-color: #F8D3D2;
  border-radius: 5px;
}

.store-text,
.name-text,
.total-cost-text {
  font-size: 16px;
  color: #323741;
}

.city-text {
  font-size: 14px;
  color: #70737A;
}

.discount-text {
  font-size: 12px;
  color: #E4504A;
}

.discount-price-text {
  font-size: 14px;
  color: #70737A;
}

.price-text {
  font-size: 14px;
  color: #323741;
}

.card {
  width: 332px;
  height: min-content;
  box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.15);
  border-radius: 15px;
}

.summary-text {
  font-size: 16px;
  color: #70737A;
}

.buy-button {
  width: 100%;
  height: 40px;
  background-color: #116530;
  border-radius: 15px;
}
</style>
