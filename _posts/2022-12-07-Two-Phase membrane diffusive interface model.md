---
layout:            post
title:             "Two-Phase Diffusive Interface Model of Biological Membranes"
date:              2022-12-07 19:27:00 +0800
tags:              Research
comments:			  true
category:          Features
catalog:    		  true
header-img: 		  "img/post-bg-e2e-ux.jpg"
header-mask:       0.3
author:            Changhao Li
---

This is the development log for a project I was recently working on.

## Formalism

Consider an closed elastic membrane, whose total Helmholtz free energy can be written as:

$$E_{el}=\int_{A}\frac{k}{2}(\kappa-c_0)^2dA \label{eq1}\tag1$$

where $k$ is the bending modulus, $\kappa(\mathbf{r})$ is the local curvature, and $c_0$ is the spontaneous curvature. Note that, in Eq($\ref{eq1}$) we neglect the contribution of surface energy and gaussian curvature.

As stated in [2008 Qiang Du et al.](https://link.springer.com/article/10.1007/s00285-007-0118-2), above energy can be reformulated in a way of phase-field modeling, by

$$ E_{el}=\int_{\Omega} \frac{k}{2\epsilon}(\epsilon\Delta\phi+(\frac{1}{\epsilon}\phi+c_0\sqrt{2})(1-\phi^2))^2dV \label{eq2}\tag2$$