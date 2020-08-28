<template>
  <div class="container">
    <div class="row">
      <div id="d1" class="col">
        <button type="button" class="btn btn-outline-primary" v-on:click="reload()">Start</button>
      </div>
    </div>
    <div class="row">
      <div class="col-sm">
        <div class="card text-center">
          <div class="card-header">Hero {{unitHero.name}}</div>
          <div class="card-body" style="height:150px">
            <img
            
              :style="{height:unitHero.percent + 'px'} "
              :src="require(`../assets/Player/${unitHero.url}`)"
              class="img-fluid"
              alt="Responsive image"
            />
          </div>
          <div class="card-footer text-muted">
            HP {{unitHero.hp}}
            <div class="progress">
              <div
                class="progress-bar"
                role="progressbar"
                :style="{width:unitHero.percent + '%'}"
                aria-valuenow="25"
                aria-valuemin="0"
                aria-valuemax="100"
              >{{unitHero.percent}}%</div>
            </div>
          </div>
        </div>
      </div>

      <div class="col-sm">
        <div class="card text-center">
          <div class="card-header">Monster {{unitMonster.name}}</div>
          <div class="card-body" style="height:150px">
            <img
              :style="{height:unitMonster.percent + 'px'}"
              :src="require(`../assets/Monster/${unitMonster.url}`)"
              class="img-fluid"
              alt="Responsive image"
            />
          </div>
          <div class="card-footer text-muted">
            HP {{unitMonster.hp}}
            <div class="progress">
              <div
                class="progress-bar"
                role="progressbar"
                :style="{width:unitMonster.percent + '%'}"
                aria-valuenow="25"
                aria-valuemin="0"
                aria-valuemax="100"
              >{{unitMonster.percent}}%</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="row">
      <div class="col" >
        <button  type="button" class="btn btn-outline-primary" v-on:click="attack(3,10),monattack(3,5)" v-if="showwinner==false">Attack</button>
        <button
          type="button"
          class="btn btn-outline-primary"
          v-on:click="attack(5,15),monattack(4,10)"
        v-if="showwinner==false">Special Attack</button>
      </div>
  </div>
   
  <div class="row">
  <div class="col">
<!-- <img
              style="height:200px"
              :src="require(`../assets/${winner.url}`)"
              class="img-fluid"
              alt="Responsive image"
            /> -->
  </div>
  </div>

  <div class="row">
  <div class="col">
      

    </div>
  </div>
  <button v-if="showwinner==true" type="button" class="btn btn-info btn-lg" data-toggle="modal" data-target="#myModal">Show winner</button>
 <div class="modal fade" id="myModal" role="dialog">
    <div class="modal-dialog">
    
      <!-- Modal content-->
      
      <div class="modal-content">
        <div class="modal-header">
          
          <h4 class="modal-title">winner</h4>
        </div>
        <div class="modal-body">
         <img
         v-if="winner.type=='Monster'"
              style="height:200px"
              :src="require(`../assets/Monster/${winner.url}`)"
              class="img-fluid"
              alt="Responsive image"
            />

            <img
         v-if="winner.type=='hero'"
              style="height:200px"
              :src="require(`../assets/Player/${winner.url}`)"
              class="img-fluid"
              alt="Responsive image"
            />
        </div>
        
      </div>
      
    </div>
  </div>
  
  


  </div>
</template>

<script>
export default {
  data() {
    return {
      unitHero: {},
      unitMonster: {},
     showwinner:false,
      Hero: [
        { name: "Anakin Skywalker",hpmax:100,hp: 100, url: "Anakin.png","percent":100,type:"hero"},
        { name: " emon ",hpmax:200,hp: 200, url: "Doraemon.jpg","percent":100,type:"hero"},
        { name: " Iron man",hpmax:150, hp: 150, url: "IronMan.png","percent":100,type:"hero"},
      ],
      Monster: [
        { name: "Thanos",hpmax:150, hp: 150, url: "Thanos.jpg","percent":100,type:"Monster"},
        { name: "Darth  vader",hpmax:180, hp: 180, url: "DarthVader.jpg","percent":100,type:"Monster"},
        { name: "Cell ",hpmax:300, hp: 300, url: "cell.jpg","percent":100,type:"Monster" },
      ],
      winner:{url:"DarthVader.jpg",type:"Monster"},
    };
  },

  methods: {
    attack: function (min, max) {
      let dmg = Math.max(Math.floor(Math.random() * max) + 1, min);
      this.unitMonster.hp = this.unitMonster.hp - dmg;
      if (this.unitMonster.hp<=0){
        this.unitMonster.hp=0
      this.winner = this.unitHero
      this.showwinner=true
      }
      this.unitMonster.percent = this.unitMonster.hp *100/this.unitMonster.hpmax
    },
     monattack: function (min, max) {
      let mondmg = Math.max(Math.floor(Math.random() * max) + 1, min);
      this.unitHero.hp = this.unitHero.hp - mondmg;
      if (this.unitHero.hp<=0){
        this.unitHero.hp=0
   this.winner = this.unitMonster
   this.showwinner=true
      }
      this.unitHero.percent = this.unitHero.hp *100/this.unitHero.hpmax
    },
    reload:function(){
      location.reload()
    }

  },
  created() {
    this.unitHero = this.Hero[Math.max(Math.floor(Math.random() * 2) + 1, 0)];
    this.unitMonster = this.Monster[
      Math.max(Math.floor(Math.random() * 2) + 1, 0)
    ];
  },
 

};
</script>

<style>
#d1{
  div.polaroid {
  width: 80%;
  background-color: white;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
}
</style>