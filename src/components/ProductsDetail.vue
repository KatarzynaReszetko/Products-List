<template>
    <div class="col-xs-12 col-md-6 col-lg-3">
        <div class="card">
            <img :src="photo" class="card-img"/>  
            <div class="card-img-overlay">
                <h6 
                    v-for="status in status.split(',')" 
                    :key="name + status" 
                    class="card-text badge badge-success float-left p-2"
                >{{ status }}</h6>
            </div>
            <div class="card-body">
                <h6 class="card-title">{{ name }}</h6>
                <hr class="hr-line">
                <h5 class="card-text new-price">{{ new_price }} zł</h5>
                <h6 :class="{invisible: !old_price}" class="card-text old-price"
                >{{ old_price }} zł</h6>
            </div>
        </div>
    </div>
</template>

<script>
export default { 
    props: ['status', 'name', 'new_price', 'old_price'],
    data() {
        return {
            photo: "https://picsum.photos/160/225?random=1",
        }
    }
}
</script>

<style scoped>
.col-xs-12, .col-md-6, .col-lg-3 {
   padding-bottom: 30px; 
}
.card-title {
    height: 65px; 
    font-weight: bold;
}
.hr-line {
    width: 40px; 
    border: 1px solid LimeGreen; 
    background-color: LimeGreen; 
    margin-bottom: 5px;
}
.new-price {
    font-weight: bold;
}
.old-price {
    text-decoration:line-through; 
    color: grey;
}
.invisible {
    visibility: hidden;
}
.badge {
    margin-right: 10px;
}
</style>