# Memory Manager Features ADR

**Status:** Incomplete

## Context


All array allocation in EEL is in a unic giant array, however someone could need more than one array.

In case that more than one array is needed it becomes necesary to use different locations in the big array as several sub arrays.


### Possible cases for array allocation

The first level on the list are categories of cases. The second level are the cases and they are mutually exclusive if they are in the same category. Third level is for cases that are contained in its parent case.

* Initialization:
    * I: It is declared in the beginning.
    * I<sup>c</sup>: It is declared on the run.
* Persistency:
    * P: It is needed for several operations.
    * P<sup>c</sup>: It is needed for just one operation.
* Deletion:
    * D<sup>c</sup>: Lasts forever.
    * D: Could be deleted.
        * d: Will be deleted.
* Ammount of data:
    * A: There is a fixed known ammount of data to be stored.
    * A<sup>c</sup>: The ammount of data to be stored is unknown while storing until finished.
* Resize:
	* R: The ammount of data changes over time.
	* R<sup>c</sup>: The ammount of data is static.

I⊆A

P<sup>c</sup>⊆d


## Decision
Objects to store:

* Type A:
   * Description:
      There is certainty that they will be used and never need be deleted enlarged or srinked.
* Type B: 
   * Description:
      They are not intended to exist forever and it is not certain that they will be needed to be deleted.
* Type C:
   * Description:
      They are known to be deleted or exist just for a short time but there could be other operations while this object exists.
* Auxiliary Memory:
   * Description:
      There is no certainty of how many data will be needed to store.
      A space where data can be stored and used within ONE operation, once used must NOT be leaved there to read later, so it can be safely overwritten or deleted. Anyway the data written here can be reclaimed to be marked as an object to prevent being overwritten/deleted.   
