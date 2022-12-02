---
layout: post
title: "Basic steps in impact analysis using LS-DYNA"
categories: dynamic
tag: 
  - dynamic
---

# Write post on ballistic impact analysis of ceramics using LS-DYNA

LS-DYNA can be a great software when doing the explicit analysis or the analysis that happen in fraction of a seconds. These type of analysis involve high impact rate or high strain rate.

## LS-DYNA workflow for impact analysis

Everything in LS-DYNA is created as the cards that are represented as the `keywords`. These `keywords` represents from geometry, materials to boundary conditions, results and studies.

**There are few basic steps that are common in all the dynamic analysis :**

- Creating the **geometry:** The geometry is created using the built-in mesh options or by importing the geometry from CAD software.
- Defining the element type and size: This is done by creating the `Section` cards. Using this, you can defined different mesh parameters of the domains.
- Defining the **material:** To create the materials, you need to select the `Material` cards. There are more than hundreds of material models defined within the LS-DYNA.
- Assigning the **materials** and **sections** to the **parts:** Once the material cards and the mesh parameters are defined, now it is the time to assign these values to the domains.
- Assigning the **boundary conditions** and **loading:** There are many ways to define the boundary conditions that vary based on the type of the boundaries. Mostly, the `Create Entity` tab. This provides options to restrains motions along multiple DOFs or to directly implement predefined constraints like welds, riveting, rigid body.
- Defining the **velocity of projectile**: No dynamic analysis is complete without defining a proper projectile velocity. The velocity is defined in many ways, but commonly `Initial` card is used to define them.
- Defining the type of **contact:** One of the most crucial step in the analysis is defining the contacts where there is relative motion between the bodies. This is done using the `Contact` cards present in LS-DYNA.
- Defining the **termination** time: Keeping termination (simulation) time too long can increase your computation cost and keeping too low can leave you without complete simulation result. The termination time can defined using the `Control` cards. In general you can estimate the simulation time by calculating the time travelled by projectile to pass the body.
- Defining the **outputs**: What data you want to retrieve from the study is defined using the `Database` cards, this includes the plots, charts, history and tables.

There are hundreds and thousands of problem specific cards present in LS-DYNA. That govern the behavior of material under loading and the response it is generating.

This includes `Control` cards for defining the energies that needs to be conserved, `EOS` cards to define the equation of state of various materials etc.

## References

* [Hypermesh LS Dyna Analysis [SPH Tutorial] - YouTube](https://www.youtube.com/watch?v=AGehqkLIHRw)

* [LS-DYNA TUTORIAL 1: Ball Impact on a Plate - YouTube](https://www.youtube.com/watch?v=3a_T7Hh19gQ&t=629s)

* [Manuals — Welcome to the LS-DYNA support site](https://www.dynasupport.com/manuals)
