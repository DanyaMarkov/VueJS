<template>
	<div>
    <div class="menu">
    Имя<input v-model="name" type="text" id="inputName" placeholder="Даниил">
      <br>
    Фамилия<input v-model="surname" type="text" id="inputSurname" placeholder="Марков">
      <br>
    Отчество<input v-model="otchestvo" type="text" id="inputOtchestvo" placeholder="Андреевич">
      <br>
    Телефон<input v-model="number" type="text" id="inputNumber" placeholder="88003448383">
      <br>
    Избранный<input v-model="checked" type="checkbox" name="a" value="1934">
      <br>
    <button id="add" v-on:click="addmember()"> Добавить</button>
   </div>

    <div class="book">
      <h2> Записная книжка : </h2>
      <div class="radio">
        <p>
          <input v-model = "radioB" v-on:click="SortNames()" id="radNam" name="sort" type="radio" checked = "checked" value="name"> По имени
        </p>
        <p>
          <input v-model = "radioB" v-on:click="SortSurnames()" id="radSur" name="sort" type="radio" value="surname"> По фамилии
        </p>
      </div>
      <ul v-html="fav">
      </ul>
      <ul v-html="def">
      </ul>
    </div>
	</div>
</template>

<script>
  export default{
    data() {
    return{
    flag : true,
    
    i: 0,

    fav : "",
    def : "",

    zapisFavNames : "",
    zapisDefSurnames : "",

    otvetFavNames : "",
    otvetDefNames : "",
    otvetFavSurnames : "",
    otvetDefSurnames : "",

    arrFavNames : [],
    arrDefNames : [],
    arrFavSurnames : [],
    arrDefSurnames  : [],

    name : "",
    surname : "",
    otchestvo : "",
    number : "",
    radioB : 1,
    checked:false
    };
    },
  
  methods: {
      addmember : function() {
      this.otvetFavNames = "";
      this.otvetDefNames = "";
      this.otvetFavSurnames = "";
      this.otvetDefSurnames = "";

      if (this.checked == true) {
          this.zapisFavNames = "<li>" + this.name + " " + this.surname + " " + this.otchestvo + " " + this.number + " ★ " + "</li>";
          this.zapisFavSurnames = "<li>" + this.surname + " " + this.name + " " + this.otchestvo + " " + this.number + " ★ " + "</li>";
          this.arrFavNames.push(this.zapisFavNames);
          this.arrFavSurnames.push(this.zapisFavSurnames);
          this.arrFavNames.sort();
          this.arrFavSurnames.sort();
      }
      else {
          this.zapisDefNames = "<li>" + this.name + " " + this.surname + " " + this.otchestvo + " " + this.number +  "</li>";
          this.zapisDefSurnames = "<li>" + this.surname + " " + this.name + " " + this.otchestvo + " " + this.number + "</li>";
          this.arrDefNames.push(this.zapisDefNames);
          this.arrDefSurnames.push(this.zapisDefSurnames);
          this.arrDefNames.sort();
          this.arrDefSurnames.sort();
      }

      this.getarr();
      this.getotvet();

    },


  SortNames: function () {
      this.radioB = 1;
      this.flag = true;
      this.getotvet();
      },

     SortSurnames: function () {
      this.radioB = 2;
      this.flag = false;
      this.getotvet();
  },

  getotvet :function () {
      if (this.flag == true) {
        this.fav = this.otvetFavNames;
        this.def = this.otvetDefNames;
      }
      else {
        this.fav = this.otvetFavSurnames;
        this.def = this.otvetDefSurnames;
      }
  },

  getarr : function () {
      for (var i = 0; i < this.arrFavNames.length; ++i) {
				this.otvetFavNames = this.otvetFavNames + this.arrFavNames[i];
			}
			for (i = 0; i < this.arrDefNames.length; ++i) {
this.otvetDefNames = this.otvetDefNames + this.arrDefNames[i];
			}
			for (i = 0; i < this.arrFavSurnames.length; ++i) {
this.otvetFavSurnames = this.otvetFavSurnames + this.arrFavSurnames[i];
			}
			for (i = 0; i < this.arrDefSurnames.length; ++i) {
this.otvetDefSurnames = this.otvetDefSurnames + this.arrDefSurnames[i];
			}
	}
  
  }

};

</script>