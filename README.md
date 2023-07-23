# RTE-Sim

Compact model for light propagation simulation in fNIRS systems

## Background



<img src="https://raw.githubusercontent.com/posvirus/Image_storage/main/img/202307231550517.png" alt="model"  />

RTE-Sim is an open-source compact model designed for light propagation simulation in functional near-infrared spectroscopy (fNIRS) systems. The goals for this compact model are:

- The model offers a more efficient alternative to traditional numerical methods like the Finite Element Method (FEM) or Monte Carlo (MC) simulation for modeling light propagation in tissues. 

- The model is compatible with mainstream circuit design tools, making it valuable for achieving comprehensive simulations of the fNIRS system's signal chain.

The model is constructed based on the analytical solution of the radiative transport equation (RTE) for uniform infinite media, where the RTE is expressed as: 

$$
\frac{1}{c_\text{m}}\cdot\frac{\partial \Phi(\vec{r},t)}{\partial t}-\kappa\nabla^2\Phi(\vec{r},t)+\mu_a\Phi(\vec{r},t)=Q(\vec{r},t)
$$

And the Green's function of the RTE $\hat{\rho}(\vec{r},\omega)$ is given by (in frequency domain):

$$
\left\{\begin{array}{l}
\displaystyle|\hat{\rho}(\vec{r},\omega)|=\frac{1}{4\pi\kappa r}\cdot\exp\left(-r\sqrt{\frac{\mu_a}{\kappa}}\right)\cdot\left(\frac{1}{\sigma r+\delta}\right)\\
\\
\displaystyle\angle\hat{\rho}(\vec{r},\omega)=\exp\left(-i\tau\omega\right),~\tau=\sqrt{\frac{\mu_a}{\kappa}}\cdot\frac{r}{2\mu_ac_\text{m}}
\end{array}\right.
$$

In this repository, we provides two implementations of this model: one in MATLAB and the other in Verilog-A.

To cite RTE-Sim in your research:

> <font face="Times New Roman" >Waiting to fulfill...</font>

## Installation

### Installation of RTE-Sim (MATLAB)

The model is composed only of SIMULINK model file ( `MATLAB\RTE_Sim.slx` ), so the installation process for MATLAB users is as simple as downloading the code. Please ensure that you have installed [SIMULINK](https://ww2.mathworks.cn/products/simulink.html) before running the model.

[Get the latest release of RTE-Sim (MATLAB)]()

### Installation of RTE-Sim (Verilog-A)

The model constructed in Verilog-A is compatible with Cadence Virtuoso's simulation environment, so users of Verilog-A model can download the model files directly and import them into the library of Cadence Virtuoso.

Moreover, users interested in the Verilog-A code can just download the specific code file (you can find it in `Verilog-A\<module_name>\veriloga\veriloga.va` ) and independently build the model.

[Get the latest release of RTE-Sim (Verilog-A)]()

## Usage

### Usage of RTE-Sim (MATLAB)

The model can be used in the same way as a ordinary SIMULINK model.

![图片1](https://raw.githubusercontent.com/posvirus/Image_storage/main/img/202307232049989.png)

The figure above illustrates the simulation of the light propagation process for a specific brain activity by configuring the parameters accordingly. Below is a list of some parameters that require configuration:

|   Parameter   |     Units     |                 Interpretation                 |
| :-----------: | :-----------: | :--------------------------------------------: |
|     `wv`      |      nm       |         Wavelength of the light source         |
|     `sp`      |      n/a      |              Scattering amplitude              |
|     `sa`      |      n/a      |                Scattering power                |
|     `cm`      |     mm/s      |           Speed of light in tissues            |
| `coef1,coef2` |      n/a      | Correction factors for the analytical solution |
|      `r`      |      mm       |            Source/detector distance            |
|   `x_base`    | mmol/mm$^{3}$ |         Baseline concentration of `x`          |
|    `x_ch`     | mmol/mm$^{3}$ |          Concentration change of `x`           |

### Usage of RTE-Sim (Verilog-A)

The model in Verilog-A comprises four sub-modules:

|    Module     |                      Interpretation                       |
| :-----------: | :-------------------------------------------------------: |
| `Core_Filter` |                Output module of the model                 |
|   `mua_Gen`   |            Generate the absorption coefficient            |
|   `mus_Gen`   |            Generate the scattering coefficient            |
| `top_module`  | Combined module of `Core_Filter`, `mua_Gen` and `mus_Gen` |

![图片2](https://raw.githubusercontent.com/posvirus/Image_storage/main/img/202307232155243.png)

![图片3](https://raw.githubusercontent.com/posvirus/Image_storage/main/img/202307232155408.png)

The model accepts a quantized voltage source as input, and the model's parameters are similar to the SIMULINK model and can be easily configured through Cadence Virtuoso's GUI:

<img src="https://raw.githubusercontent.com/posvirus/Image_storage/main/img/202307232217351.png" alt="图片4" style="zoom:67%;" />

## Maintainers

[@Wenyao Chen](https://github.com/posvirus).

##Contributors

This project exists thanks to all the people who contribute.

