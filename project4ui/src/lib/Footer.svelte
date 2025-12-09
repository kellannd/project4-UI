<script>
    export let currPage

    export let requestsForUser
</script>

<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.2/font/bootstrap-icons.css"
/>

<div
  style="position:absolute; bottom:0px; margin-bottom: -1px; height:75px; left:0px; right:0px; overflow:hidden; border-top: 2px solid black; background-color: #efefef"
>
  <div class="footer-buttons">
    <div class="{currPage === 'main' ? 'active' : ''}" style="height: 75px; display: flex; justify-content: center; align-items: center; border-right: 2px solid black">
      <button style="background-color: transparent; border: none" onclick={() => {
        currPage = "main"
        requestsForUser()
      }}>
      <i style="font-size: 40px; font-weight:bold" class="bi bi-plus-circle"></i>
      </button>
    </div>


    <div class="{currPage === 'requests' ? 'active' : ''}" style="height: 75px; display: flex; justify-content: center; align-items: center; border-right: 2px solid black">
      <button style="background-color: transparent; border: none" onclick={() => currPage = "requests"}>
      <i style="font-size: 40px" class="bi bi-list-task"></i>
      </button>
    </div>

    <div class="{currPage === 'messages' ? 'active' : ''}" style="height: 75px; display: flex; justify-content: center; align-items: center; border-right: 2px solid black">
      <button style="background-color: transparent; border: none" onclick={() => currPage = "messages"}>
      <i style="font-size: 40px" class="bi bi-chat"></i>
      </button>
    </div>


    <div class="{currPage === 'user' ? 'active' : ''}" style="height: 75px; display: flex; justify-content: center; align-items: center">
        <button style="background-color: transparent; border: none" onclick={() => currPage = "user"}>
      <i style="font-size: 40px" class="bi bi-person-fill"></i>
      </button>
    </div>


  </div>

</div>

<style>
  @import "../app.css";
  .footer-buttons {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
  }

  .footer-btn {
    background-color: bisque;
    height: 75px;
  }

  .footer-btn:hover {
    background-color: blueviolet;
  }

  .active {
  background-color: #cacaca;
  }
</style>
