# Catalog Drive Coding Question

## Secret Sharing Test

### Overview

This project uses Lagrange interpolation to show how to solve a secret sharing dilemma. The idea was influenced by polynomial interpolation, in which a predetermined number of shares are needed to rebuild the original secret after secret material is divided among several parties.

#### Problem Statement

The objective is to use Lagrange interpolation to calculate a polynomial's value at a certain point. To accomplish this, data points in the supplied JSON file must be processed. To be precise, the tasks are:

1. **Convert Base-Specific Values**: Convert numbers provided in different bases to decimal.
2. **Apply Lagrange Interpolation method**: Using the transformed data points, get the value of the polynomial at {x = 0}.
