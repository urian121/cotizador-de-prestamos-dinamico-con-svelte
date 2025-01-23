<script>

// Impotar Bootstrap CSS y sus iconos
import "bootstrap/dist/css/bootstrap.min.css";
import "bootstrap-icons/font/bootstrap-icons.css";

  import Header from "./components/Header.svelte";
  import Buttom from "./components/Buttom.svelte";
  import { formatearDinero, calcularTotalPagar } from "./helpers/index.js";

  let cantidad = 8000;
  let meses = 6;
  let total = 0;
  let pago = 0;

  const MIN = 0;
  const MAX = 20000;
  const STEP = 100;

  $: {
    total = calcularTotalPagar(cantidad, meses);
  }

  $: {
    pago = total / meses;
  }

  $: {
    cantidad = cantidad;
  }

  function handleChange(e) {
    cantidad = +e.target.value;
    console.log('Cantidad deslizada:', cantidad);
  }

  function handleClickDecremento() {
    const valor = cantidad - STEP;
    console.log('Cantidad decrementada:', cantidad);
    cantidad = valor;
  }

  function handleClickIncremento() {
    const valor = cantidad + STEP;
    cantidad = valor;
    console.log('Cantidad incrementada:', valor);
  }
</script>

<div class="container mt-2">
  <Header />
<div class="d-flex justify-content-between">
  <Buttom operador="-" cantidad={cantidad} fn={handleClickDecremento} />
  <Buttom operador="+" cantidad={cantidad} fn={handleClickIncremento} />
</div>

<div class="range">
<input
  type="range"
  class="form-range custom-range"
  on:input={handleChange}
  min={MIN}
  max={MAX}
  step={STEP}
  bind:value={cantidad}
/>
</div>

  <p class="text-center my-3 valor-prestamo">
    {formatearDinero(cantidad)}
  </p>

  <h2 class="text-center text-secondary fw-bold mt-3">
    Elige un <span class="text-primary">Plazo </span> a pagar
  </h2>

 <select
  class="form-select mt-3"
  bind:value={meses}
>
  <option value="6" selected>6 Meses</option>
  <option value="12">12 Meses</option>
  <option value="24">24 Meses</option>
</select>

  <div class="card bg-light mt-4 border-0">
    <div class="card-body text-center">
      <h2 class="card-titletext-secondary fw-bold">
        Resumen <span class="text-primary">de pagos</span>
      </h2>
      <p class="card-text h4 fw-bold">{meses} Meses</p>
      <p class="card-text h3 fw-bold"><span style="color: #f50;">{formatearDinero(total)}</span> Total a pagar</p>
      <p class="card-text h3 fw-bold"><span style="color: #f50;">{formatearDinero(pago)}</span> Mensuales</p>
    </div>
  </div>
</div>

<style>

/* custom input range */
input[type="range"] {
  -webkit-appearance: none;
  appearance: none; 
  width: 100%;
  cursor: pointer;
  outline: none;
  overflow: hidden;
  border-radius: 16px;
}

/* Track: webkit browsers */
input[type="range"]::-webkit-slider-runnable-track {
  height: 15px;
  background: #ccc;
  border-radius: 16px;
}

/* Track: Mozilla Firefox */
input[type="range"]::-moz-range-track {
  height: 15px;
  background: #ccc;
  border-radius: 16px;
}
.form-range{
  height: auto ! important;
}

/* Thumb: webkit */
input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none; 
  height: 15px;
  width: 15px;
  background-color: #fff;
  border-radius: 50%;
  border: 2px solid #f50;
  /*  slider progress trick  */
  box-shadow: -407px 0 0 400px #f50;
}

input[type="range"]::-moz-range-thumb {
  height: 15px;
  width: 15px;
  background-color: #fff;
  border-radius: 50%;
  border: 1px solid #f50;
  /*  slider progress trick  */
  box-shadow: -407px 0 0 400px #f50;
}

.range {
  display: flex;
  align-items: center;
  max-width: 500px;
  height: 4rem;
  width: 100%;
  background: #fff;
}
/* fin custom input range */
</style>