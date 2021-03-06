The following files contain the dataset used in the paper

Fader, Peter S. and Bruce G.S. Hardie (1996), "Modeling Consumer Choice Among 
SKUs," Journal of Marketing Research, 33 (November), 442-452.


Quoting from p. 446 of the paper,

The data come from an IRI panel in Philadelphia and cover the period from 
January 1990 to June 1992. The only criterion for inclusion in our data set is 
that the household must have made at least one purchase in 1991. This gives us 
594 qualifying households that made a total of 9781 purchases over the 2.5-
year period. The 3227 purchases from 1990 are used for initializing model 
variables, and the 4417 purchases from 1991 are used for model calibration. 
The remaining 2137 purchases made during the first half of 1992 are used for 
forecasting purposes.

The specific files and their associated formats are as follows: 

D1PUR.DAT 

   * Contains the household purchase history data.

   * Two fields: HH_id  trip_info 
    
   * The format of the trip_info variable is AAABBBCCC where
    
        AAA = IRI week
        BBB = store#
        CCC = SKU# purchased
        
        
MERCH.DAT

   * Contains store environment info.

   * Five fields: SKU#  store#  IRIweek  price_paid  merchandising
    
   * An SKU's presence is indicated by price_paid >= 0.02.
    
   * The format of the merchandising variable is AAABCD where
    
        AAA = depromoted price
        B   = ignore
        C   = display
        D   = feature
        
   * In our models, we use dummies for feature and display:
    
        DISP = 1 if C >= 1; 0 otherwise
        FEAT = 1 if D >= 1; 0 otherwise
        
   * We also separate price into depromoted (regular_price) and price_cut
     components:
    
        regular_price = AAA
        price_cut = AAA - price_paid (if the result is < 0, price_cut = 0)
        
   * Before including regular_price or price_cut in the model, we divide each
     number by the SKU's ARSP (average regular selling price) in that store.

    
ARSP.DAT

   * Contains the average regular selling price of each SKU in each store.

   * Three fields: SKU#  store#  ARSP


BRSINFO.DAT

   * Contains the attribute information for each SKU.

   * Eleven fields: SKU#  description_of_SKU  brand  form  formula1 formula2
                    size  brand#  form#  formula2#  size#

   * The IRI stub gave us nine "formulas" (formula1); we collapsed these to four
     (formula2).

   * We request that users of this dataset use the attribute structure presented
     in the paper (i.e., use formula2 instead of formula1).

   * The alert reader will note that this file contains 59 records while the
     paper refers to 56 SKUs. Two of the three "missing" SKUs are due to the
     fact that different sizes (as measured in sheet counts or fluid oz.) are
     coded as belonging to the same size category. The third is due to the
     collapsing of formula1 to formula2.

   * In the models we estimated, the reference levels for each attribute (i.e.,
     coeff. constrained to 0) were:

        Brand   - PVL (7)
        Form    - S   (4)
        Formula - RG  (2)
        Size    - SM  (1)


IRIweek.xls

   * Time is week of purchase recorded as IRI week; this is a measure used by
     IRI where week 1 corresponds to the week ending 09/09/79. This spreadsheet
     provides a mapping of IRI weeks to dates.


Miscellaneous:

   * Our model makes use of "loyalty" variables, which require an intialization
     period. The initialization period starts (IRI) week 540. The calibration
     period runs from 592-643.  The "forecast" period is week 644 onwards.
