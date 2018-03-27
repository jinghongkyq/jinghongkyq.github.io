#### Slice layer 

Decompose `bottom` into several `tops` (Split layer copies `bottoms`, output to `tops`).
```
layer {
  name: "slice"
  type: "Slice"
  bottom: "input"
  top: "output1"
  top: "output2"
  top: "output3"
  top: "output4"
  slice_param {
    axis: 1
    slice_point: 1
    slice_point: 3
    slice_point: 4
  }
}
```
given the dimention of bottom: `N*5*H*W`, the dimentions of output tops are `N*1*H*W N*2*H*W N*1*H*W N*1*H*W`, respectively.
`axis` indicates the target axis;     
`slice_point` indicates indexes in the selected dimension (the number of indices must be equal to the number of top blobs minus one).

#### Silence layer

layer {
  name: "silence_name"
  type: "Silence"
  bottom: "silence_layer"
  phase: "TRAIN"
}
