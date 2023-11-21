# https://btholt.github.io/complete-intro-to-react-v6/useref

## useRef
Dia tidak menunggu satu cycle dia langsung terupdate. Tidak seperti useState karena useState perlu 1 kali cycle dia baru terupdate datanya.


## useReducer
Ini mirip sekali dengan Redux. Tapi the proper way to use useReducer when the variable is global so it's better using redux, and when it's for local area better use useReducer.

```sh
import { useReducer } from "react";

// fancy logic to make sure the number is between 0 and 255
const limitRGB = (num) => (num < 0 ? 0 : num > 255 ? 255 : num);

const step = 50;

const reducer = (state, action) => {
  switch (action.type) {
    case "INCREMENT_R":
      return Object.assign({}, state, { r: limitRGB(state.r + step) });
    case "DECREMENT_R":
      return Object.assign({}, state, { r: limitRGB(state.r - step) });
    case "INCREMENT_G":
      return Object.assign({}, state, { g: limitRGB(state.g + step) });
    case "DECREMENT_G":
      return Object.assign({}, state, { g: limitRGB(state.g - step) });
    case "INCREMENT_B":
      return Object.assign({}, state, { b: limitRGB(state.b + step) });
    case "DECREMENT_B":
      return Object.assign({}, state, { b: limitRGB(state.b - step) });
    default:
      return state;
  }
};

const ReducerComponent = () => {
  const [{ r, g, b }, dispatch] = useReducer(reducer, { r: 0, g: 0, b: 0 });

  return (
    <div>
      <h1 style={{ color: `rgb(${r}, ${g}, ${b})` }}>useReducer Example</h1>
      <div>
        <span>r : {r} </span>
        <button onClick={() => dispatch({ type: "INCREMENT_R" })}>➕</button>
        <button onClick={() => dispatch({ type: "DECREMENT_R" })}>➖</button>
      </div>
      <div>
        <span>g : {g} </span>
        <button onClick={() => dispatch({ type: "INCREMENT_G" })}>➕</button>
        <button onClick={() => dispatch({ type: "DECREMENT_G" })}>➖</button>
      </div>
      <div>
        <span>b : {b} </span>
        <button onClick={() => dispatch({ type: "INCREMENT_B" })}>➕</button>
        <button onClick={() => dispatch({ type: "DECREMENT_B" })}>➖</button>
      </div>
    </div>
  );
};

export default ReducerComponent;
```

## useMemo
Ini digunakan untuk menyimpan nilai, ini sangat bagus digunakan ketika ada komputasi yang sangat berat.

Kita istilahkan seperti code dibawah yaitu fibonacci, dan function yang digunakan adalah recursive. Pada fibonacci ke 40 dia akan sangat berat.
Jadi ketika kita memiliki action klik ganti warna semisal. Dia akan mengeksekusi function fibonacci sekali lagi dengan nilai 40 yang akan memakan waktu lama padahal kita hanya ingin mengganti warna.

Oleh karena itu digunakan useMemo yang mana kita akan mengecek apakah num berubah ? Kalau tidak berubah kita tidak perlu melakukan komputasi dan cukup mereturn data yang lama.
```sh
  const [num, setNum] = useState(1);
  const fib = useMemo(() => fibonacci(num), [num]);
```

## useCallback
Ini sama kayak useMemo

## useLayoutEffect
Ini sama halnya dengan useEffect akan tetapi dia tidak perlu menunggu cycle berjalan. Akan tetapi langsung seperti useRef. Ini sangat baik digunakan ketika kita membuat sebuah animasi yang harus segera menghasilkan nilai ketika kita mengubah textarea atau lain lain.
