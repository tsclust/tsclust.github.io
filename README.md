# tsclust.opt_tsclust.OptTSClust

class tsclust.opt_tsclust.OptTSClust(k: int,  scheme: str = 'z1c0',  n_allow_assignment_change: None|int = None,  is_Z_positive: bool = True,  is_tight_constraints: bool = True,     lagrangian_multiplier: int = 0, use_sum_distance: bool = False, warm_start: bool = True,  normalise_assignment_penalty: bool = True, strictly_n_allow_assignment_change: bool = False, 
 use_MILP_centroid: bool = True, use_full_constraints: bool = True, IFrac: float = 0.2, top_n_percentile: float = 0.0, max_iter: int = 10, random_state: None|int = None, add_constraint_per_cluster: bool = True, init_with_prev: bool = True) 

        
        Class for optimal time-series clustering. Throughout this doc and code, 'z' refers to cluster centers, while 'c' to label assignment.
        This creates an OptTSClust object

        k: int
            number of clusters
        scheme: {'z0c0', 'z0c1', 'z1c0', 'z1c1'}, default='z1c0'
            the scheme to use for tsclustering. 
            'z0c0': fixed center, fixed assignment, 
            'z0c1': fixed center, changing assignment, 
            'z1c0': changing center, fixed assignment, 
            'z1c1': changing center, changing assignment
        n_allow_assignment_change: int or None, default=None
            total number of label changes to allow
        is_Z_positive: bool, default=True
            True means assume non-negativity constraint for z. The scale of the final results are not affected since OptTSClust will return solutions in the original scale of the input data.
            Setting this to True often leads to speedup. See ... for more details.  
        is_tight_constraints: bool, default=True
            Indicate if to use use tight bounds (the bounding box of the data) for z and the objective value
        lagrangian_multiplier: int, default=0
            The penalty term for constrained label changes. Value should be in range [0, np.inf], the higher the value, the less
            the number of label changes allowed
        use_sum_distance: bool, default=False
            Indicate if to use sum of distance to cluster as the objective. This is the sum of the distances between points in a time series
            and their centroids. 
        warm_start: bool, default=True
            Indicates if to use k-means to initialize the centroids (Z) and their assignments (C).
        normalise_assignment_penalty: bool, default=True
            Indicate if to normalize the penalty term when using lagrangian_multiplier
        strictly_n_allow_assignment_change: bool, default=False
            If True, indicate if to use n_allow_assignment_change constraint as an active constraint.
        use_MILP_centroid: bool, default=True
            If True, cluster_centers_ atrribute will be cluster centers obtained from MILP solution, else the average of the 
            datapoints per timestep
        use_full_constraints: bool, default=True
            If True, use all the samples as constraints. If False, use constraint generation. When using constraint generation, 
            subsamples are being used as constraints with samples added to the constraints until optimal solution is found.
        IFrac: float, default=0.2
            fraction of samples to use as initial constraints when using constraint generation.
        top_n_percentile: foat, default=0.0
            percentile of most violated constraints to add to constraints when using constraint generation. 
            Value should in range [0, 1]. Note that a value of 0 means to use the most violated constraint. 
        max_iter: int, default=10
            Maximum number of iterations to use when using constraint violation.
        random_state: int, default=None
            Set the random seed used when initializing with k-means or when initializing samples when using constraint generation.
        add_constraint_per_cluster: bool, default=True
            If True, top_n_percentile constraints are being from each cluster when using constraint generation. 
        init_with_prev: bool, default=True
            If True, use the solution from previous iteration as initial solution for the next iteration when using constraint generation        
        
