---
layout: default
title: HazardousBody
---

The `HazardousBody { }` subnode of the `Body { }` node indicates that the body is hazardous, and thus, the body will gradually apply heat to the vessel as the vessel nears the body. It replaces `HazardousOcean { }` as the `HazardousBody { }` has more fine control and detail.

**Example**
```
Body
{
  HazardousBody
  {
    Item
    {
      ambientTemp = 270
      biomeName = Sargasso Seas
      sumTemp = true
      HeatMap = MyMod/PluginData/MyPlanet/heatmap.dds
      
      AltitudeCurve
      {
        key = 0 1
        key = 20000 0.9
        key = 40000 0.75
        key = 75000 0.5
        key = 100000 0.35
        key = 150000 0.1
        key = 200000 0
      }
      LatitudeCurve
      {
        key = -75 0.1
        key = -30 0.7
        key = 0 1
        key = 30 0.7
        key = 75 0.1
      }
      LongitudeCurve
      {
        key = -160 1
        key = -125 0.2
        key = -75 0.8
        key = -35 0.3
        key = 0 1
        key = 35 0.5
        key = 75 0.9
        key = 125 0.1
        key = 165 0.6
      }
    }
    Item // this item creates an actual torus shape resembling a Van Allen belt
    {
      ambientTemp = 1250
      AltitudeCurve
      {
        key = 270000 0 0 0
        key = 570000 1 0 0
        key = 2070000 0.2 0 0
        key = 2970000 1 0 0
        key = 3240000 1 0 0
        key = 7270000 0.2 -2E-07 -2E-07
        key = 9750000 0 0 0
      }
      LatitudeCurve
      {
        key = -60 0 0 0
        key = 0 1 0 0
        key = 60 0 0 0
      }
    }
  }
}
```

|Property|Format|Description|
|--------|------|-----------|
|sumTemp|Boolean|LOOK AT CODE/ASK SIGMA|
|biomeName|String|Optional. This limits this instance of HazardousBody to the specified biome.|
|ambientTemp|Double|Optional, defaults to 0. This is the base temperature before applying modifiers such as the Alt/Lon/Lat Curves and the HeatMap. After all such modiers are applied, if the new temperature is higher than KSP's default ambient temperature, then the new one will be applied. If KSP's is higher, KSP's shall be used instead.|
|HeatMap|File Path|Optional. A greyscale map for fine control of the ambient temperature. It acts as a multiplier map. Black = 0, White = 1.|
|AltitudeCurve|FloatCurve|Optional, the heat multiplier defaults to 1 at all altitudes. Note that altitude itself is measured from the center of the body, not from sea level so the body radius must be added to the X values of all keys given here. |
|LatitudeCurve|FloatCurve|Optional, the heat multiplier defaults to 1 at all latitudes. The range for X values is -90 ~ 90. |
|LongitudeCurve|FloatCurve|Optional, the heat multiplier defaults to 1 at all longitudes. The range for X values is -180 ~ 180. |
