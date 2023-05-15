<script>
let num = 2,
  timeout = false,
  seconds = 0,
  inputnum = 2,
  solvetimeout = false,
  currentnum = 2,
  iterations = 0,
  heighest_point = 2;

function collatz() {
  if (num == 1) return stop_collatz();
  if (num % 2 == 0) {
    num /= 2;
  } else {
    num = num * 3 + 1;
  }
  iterations++;
  if (num > heighest_point) heighest_point = num;
}

function start_collatz() {
  stop_collatz();
  num = inputnum;
  timeout = setInterval(collatz, seconds * 1000);
}

function stop_collatz() {
  clearInterval(timeout);
  timeout = false;
}

function solve_mode() {
    num = currentnum=2;
    heighest_point = iterations=0;
    solve();
}

function solve() {
    solvetimeout = setInterval(function () {
        while(num!=1){
            if (num % 2 == 0) {
                num /= 2;
            } else {
                num = num *3 +1;
            }
            iterations++;
            if (num > heighest_point) heighest_point = num;
        }
        currentnum++;
        num=currentnum;
    }, seconds *1000);
}
</script>
<p>Interval between each run: </p><input type="text" placeholder='interval' bind:value={seconds}><br>
<p>number: </p><input type="number" placeholder="enter number" bind:value={inputnum}><br>
{#if !timeout}
{#if inputnum > 1}
<br>
<button on:click={start_collatz}>start</button>
{:else}
<p>enter a number greater than 1</p>
{/if}
{:else}
<button on:click={function(){stop_collatz();num=1}}>stop</button>
{/if}
<p>Iterations/steps: {iterations}</p>
<p>Heighest point: {heighest_point}</p>
{#if solvetimeout}
<h1>current number: {currentnum}</h1>
<p>trying: {num}</p>
<br><br><br>
<button on:click={function(){clearTimeout(solvetimeout);solvetimeout=false;num=2;currentnum=2;inputnum=num; iterations=0}}>stop solving</button>
{:else}
<h1>{num>2?num:inputnum}</h1>
<br><br><br><br><br><br>
<button on:click={solve_mode}>solve mode</button>
{/if}
<style>
    :global(body){
        text-align: center;
    }
</style>