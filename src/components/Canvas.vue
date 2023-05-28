<template>
    <canvas id="canvas"></canvas>
</template>

<script>
export default {
    name: 'Canvas',
    props:['table',"cpt"],
    data(){
        return{
            canvas:null,
            ctx:null,
            updown:false,
        }
    },
    mounted(){
        this.canvas=document.getElementById('canvas')
        this.ctx=this.canvas.getContext("2d")

        this.canvas2=document.getElementById('canvas')
        this.ctx2=this.canvas.getContext("2d")

        this.resize()
        this.draw()
    },
    updated(){
        this.deleteCanvas()
        if(this.cpt==0){
            this.draw_0()
        }else{
        this.draw()
        }
    },
    methods:{
        resize(){
            this.canvas.width=this.canvas.clientWidth
            this.canvas.height=this.canvas.clientHeight
        },
        draw_0(){
            this.ctx.beginPath()
            this.ctx.strokeStyle = 'black'
            this.ctx.lineWidth="2"
            this.ctx.moveTo(50,20)
            this.ctx.lineTo(1050,20)
            this.ctx.stroke()

            this.ctx.font = 'bold 18px Arial'
            this.ctx.fillStyle="black"
            this.ctx.fillText('- 600',2,28)

            this.ctx.font = 'bold 18px Arial'
            this.ctx.fillStyle="black"
            this.ctx.fillText('0',50+(525/2),45)
            this.ctx.font = 'bold 18px Arial'
            this.ctx.fillStyle="black"
            this.ctx.fillText('500',50+((525*2)/2),45)


            this.ctx.font = 'bold 18px Arial'
            this.ctx.fillStyle="black"
            this.ctx.fillText('1000',50+((525*3)/2),45)

            this.ctx.font = 'bold 18px Arial'
            this.ctx.fillStyle="black"
            this.ctx.fillText('1500',1055,28)

            this.table.map(val =>{
                if(val.id <= 10){
                    this.ctx.beginPath()
                    this.ctx.strokeStyle = 'black'
                    this.ctx.lineWidth="1"
                    this.ctx.moveTo((100+600+val.date)/2.1,20)
                        
                    if(this.updown){
                        this.ctx.lineTo((100+600+val.date)/2.1,0)
                        this.updown = !this.updown
                    }else{
                        this.ctx.lineTo((100+600+val.date)/2.1,40)
                        this.updown = !this.updown
                    }
                    this.ctx.stroke()
                }
            })
        },
        draw(){
            this.ctx.beginPath()
            this.ctx.strokeStyle = 'black'
            this.ctx.lineWidth="2"
            this.ctx.moveTo(50,20)
            this.ctx.lineTo(1050,20)
            this.ctx.stroke()

            let x = 1500+(this.cpt-1)*100
            let y = 1500+this.cpt*100

            this.table.map(val =>{
                if((val.date>x) && (val.date<y)){  
                    this.ctx.beginPath()
                    this.ctx.strokeStyle = 'black'
                    this.ctx.lineWidth="1"
                    this.ctx.moveTo(50+(val.date- x )*10,20)
                        
                    if(this.updown){
                        this.ctx.lineTo(50+(val.date-x)*10,0)
                        this.updown = !this.updown
                    }else{
                        this.ctx.lineTo(50+(val.date-x)*10,40)
                        this.updown = !this.updown
                    }
                    this.ctx.stroke()
                }
            })
            this.ctx.font = 'bold 18px Arial'
            this.ctx.fillStyle="black"
            this.ctx.fillText(x,2,28)

            this.ctx.font = 'bold 18px Arial'
            this.ctx.fillStyle="black"
            this.ctx.fillText(y,1055,28)
        },
        deleteCanvas(){
            this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height);
        }
    }
}
</script>

<style scoped>
    canvas{
        width:1100px; 
        height:50px;
    }
</style>
