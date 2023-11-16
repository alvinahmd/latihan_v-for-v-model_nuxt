<!-- eslint-disable vue/require-v-for-key -->
<template>
  <div>
    <div class="flex flex-row w-full">
      <div class="bg-slate-900 w-80 h-screen" />
      <div class=" w-full flex flex-col">
        <div class="w-full overflow-x-auto px-8">
          <div class="py-4">
            <button class="border-2 border-blue-700 px-2 py-2 rounded-lg" @click="tambahData">
              Tambah Data Baru
            </button>
          </div>
          <table class=" w-full table-auto border border-collapse border border-slate-500 ">
            <thead>
              <tr class="">
                <th class=" w-1/4  border border-slate-500 text-xl text-slate-500 font-bold">
                  Nama
                </th>
                <th class="border border-slate-500 text-xl text-slate-500 font-bold">
                  Alamat
                </th>
                <th class="border border-slate-500 text-xl text-slate-500 font-bold">
                  Agama
                </th>
                <th class="border border-slate-500 text-xl text-slate-500 font-bold">
                  Jurusan
                </th>
                <th class="border border-slate-500 text-xl text-slate-500 font-bold">
                  No.Hp
                </th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(item, index) in items" :key="index">
                <td class=" py-2 px-2 border border-slate-500 text-base text-blue-700 font-medium font-sans">
                  <input v-model="items[index].name" type="text" class="">
                </td>
                <td class="border px-2 border-slate-500 text-base text-blue-700 font-medium font-sans">
                  <input v-model="items[index].alamat" type="text" class="">
                </td>
                <td class="border px-2 border-slate-500 text-base text-blue-700 font-medium font-sans">
                  <select v-model="items[index].selectedAgama">
                    <option v-for="agama in agamaOptions" :key="agama.id" :value="agama.id">
                      {{ agama.label }}
                    </option>
                  </select>
                </td>
                <td class="border px-2 border-slate-500 text-base text-blue-700 font-medium font-sans">
                  <select v-model="items[index].selectedJurusan">
                    <option v-for="jurusan in jurusanOptions" :key="jurusan.id" :value="jurusan.id">
                      {{ jurusan.label }}
                    </option>
                  </select>
                </td>
                <td class="border px-2 border-slate-500 text-base text-blue-700 font-medium font-sans">
                  <input v-model="items[index].hp" type="text" class="" @input="validatePhoneNumber(index)">
                  <pre v-if="items[index].erorhp" style="color:red">{{ items[index].erorhp }}</pre>
                </td>
              </tr>
            </tbody>
          </table>
          {{ items }}
        </div>
        <div class="pt-14 px-8">
          <h1 class="text-xl font-bold text-slate-700">
            Pencatatan keuangan
          </h1>
          <div class="w-full pt-14 ">
            <div class="pb-8">
              <input type="date" name="tanggal" class="w-full border-b border-blue-700 focus focus:outline-none apperance-none">
            </div>
            <div class="pb-8">
              <input placeholder="masukkan pemsukkan" type="text" class="text-sm text-slate-800  font-sans w-full border-b border-blue-700 focus focus:outline-none apperance-none">
            </div>
            <div class="">
              <input placeholder="masukkan penggeluaran" type="text" class="text-sm text-slate-800  font-sans w-full border-b border-blue-700 focus focus:outline-none apperance-none">
            </div>
            <div class="pt-8 ">
              <p>
                Hasil = ......
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    // eslint-disable-next-line no-labels
    return {
      items: [
        { name: 'alvin', alamat: 'Sumbergedong', selectedAgama: 'islam', jurusan: 'informatika', hp: '0888432425', erorhp: null }
        // ... data lainnya
      ],
      agamaOptions: [
        { id: 'islam', label: 'Islam' }
        // ... opsi agama lainnya
      ],
      jurusanOptions: [
        { id: 'informatika', label: 'Informatika' },
        { id: 'tata boga', label: 'tata boga' }
        // ... opsi jurusan lainnya
      ],
      selectedAgama: '', // Properti untuk menyimpan agama yang dipilih
      selectedJurusan: '' // Properti untuk menyimpan jurusan yang dipilih
    }
  },
  methods: {
    tambahData () {
      // Data baru yang akan ditambahkan
      const newData = { name: 'baru', alamat: 'Sumbergedong', agama: this.selectedAgama, jurusan: this.selectedJurusan, hp: '08123456789', erorhp: null }

      // Menambahkan data baru ke dalam array items
      this.items.push(newData)

      // Update opsi agama setelah penambahan data baru
      if (!this.agamaOptions.some(opt => opt.id === this.selectedAgama)) {
        this.agamaOptions.push({ id: this.selectedAgama, label: this.selectedAgama })
      }

      // Update opsi jurusan setelah penambahan data baru
      if (!this.jurusanOptions.some(opt => opt.id === this.selectedJurusan)) {
        this.jurusanOptions.push({ id: this.selectedJurusan, label: this.selectedJurusan })
      }
    },
    validatePhoneNumber (index) {
      const phoneNumber = this.items[index].hp
      const Regex = /^(?:(?:\+|0{0,2})62(\s*-]\s*)?|[0]?)?[62789]\d{9}$/

      if (!phoneNumber) {
        this.items[index].erorhp = 'Phone Number field cannot be empty'
      } else if (!Regex.test(phoneNumber)) {
        this.items[index].erorhp = 'Invalid phone number'
      } else {
        this.items[index].erorhp = ''
      }
    }
  }
}
</script>
