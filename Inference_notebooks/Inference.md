# Inference Time

### Ensembles

- Did the ensembles of different models trained, tried average ensemble.
- Ensembling the models increased the fbeta score from 65 to 74.
- Tried weighted ensembles tooo

### TTA

- Performed TTA(Test Time Augmentations) during the final inference.
- This included the rotation of the image during the inference.(did 90,180,270,360 degree roatations)
        
          x = [x, *[tc.rot90(x, k=i, dims=(-2, -1)) for i in range(1, 4)]]
          x = tc.cat(x, dim=0)
            
- after predicting on these augmentations, again rotated the output then took the average of the outputs

          x=[tc.rot90(x[i],k=-i,dims=(-2,-1)) for i in range(4)]
          x=tc.stack(x,dim=0)


### 8 Channels average score

- Out of the 65 channels, the center channels contained the information.
- So took the center 8 channels and made them into group of 3 because the model trained took only 3 channels in input
- The groups of 3 channels were (1,2,3) , (4,5,6) , (6,7,8)
- So this resulted in output of 3 masks which was later averaged to get the final mask


