<script>
    import logo1 from "../assets/PoP (1).png";
    import logo2 from "../assets/PoP (2).png";
</script>

<div style="position:absolute; top:0px; left:0px; height:75px; right:0px;overflow:hidden; background-color: #efefef">
<div class="header">
        <div>
        <img src={logo1} style="height: 75px" />
    </div>

    <div style="display: flex; justify-content: center; align-items: center">
        <h1>app</h1>
    </div>

    <div>
        <img src={logo2} style="height: 75px; position: absolute; right: 0px" />
    </div>
    </div>
</div>

<style>
.header {
    display: grid;
    grid-template-columns: 1fr 3fr 1fr;
}

    </style>
