# dynamiccolorgraphing

printf("Enter no. of colours :: ");
	scanf("%d",&c);
	
	//Graph Colouring
	//counting number of edges connected to each vertex
	for(i=0;i<v;i++)
	{
		count = 0;
		for(j=0;j<v;j++)
		{
			if(edgesInput[i][j] == 1)
			count += 1; 
		}
		numEdge[i] = count;
	}
	//Displaying the number of edges
	for(i=0;i<v;i++)
	{
		printf ("%d ",numEdge[i]);
	}
	printf("\n");
	//Determining vertex with max number of edges
	for(i=0;i<v;i++)
	{
		if (numEdge[i] > maxE)
		{
			maxE = numEdge[i];
			vMaxE = i+1;
		}
	}
	printf("Vertex with max edges is Vertex %d\n",vMaxE);
	//Colouring
	//Declaring Colour matrix
	int **color = (int **)malloc(v*sizeof(int *));
	
	//Checking if colour can be same or not
	for(i=0;i<v;i++)
	{
		color[i] = (int *)malloc(v*sizeof(int));
		for(j=0;j<v;j++)
		{
			if (edgesInput[i][j]==1)
				color[i][j] = 2;				
			else
				color[i][j] = 1;
		}
	}
	
	for(i=0;i<v;i++)
	{
		for(j=0;j<v;j++)
			printf("%d",color[i][j]);
		printf("\n");
	}
	//Assigning vertex with max edges as Color 1

	//initialize all values to 0	
	for(i=0;i<v;i++)
		colorGraph[i] = 0;

	//Initializing colour	
	int assignedcolor = 1;
	colorGraph[vMaxE-1] = 1;	

	
	//Assigning Color to vertices by checking color is same or not
	for(i=0;i<v;i++)
	{
		printf("%d\n",i);
		for(j=0;j<v;j++)
		{			
			if(i != j)
			{
				if(color[i][j]==1)
				{			
					//Checking if adjacent vertex has same color
					for(int k = 0;k<v;k++)
					{
						if (j != k && edgesInput[j][k] == 1)
							{
								if (colorGraph[k]!=colorGraph[i] )
									{
										if (colorGraph[j] !=0 )
										{
											if(i!=0 && i<v-1 && colorGraph[i-1] != colorGraph[j] && colorGraph[i+1]!=colorGraph[j])
												colorGraph[i]=colorGraph[j];
											else if(i==0 && colorGraph[i+1]!=colorGraph[j])
												colorGraph[i]=colorGraph[j];
											else if(i==v-1 && colorGraph[i-1]!=colorGraph[j])
												colorGraph[i]=colorGraph[j];
										}
										else if(colorGraph[j]==0)
											colorGraph[j]=colorGraph[i];
									}
							}
					}
					if(colorGraph[j]==0)
						colorGraph[j]=colorGraph[i];
				}	
				else if(color[i][j]==2)
				{
					if (colorGraph[j] == 0)
					{					
						assignedcolor +=1;
						colorGraph[j] = assignedcolor;
					}
					else if (colorGraph[j] != 0)
					{
						if (colorGraph[j] == colorGraph[i])
						{
							//checking the highest value of color
							int hcol = 1;
							for(int c=0;c<v;c++)
							{
								if(colorGraph[c]>hcol)
									hcol = colorGraph[c];
							}
							
							colorGraph[j] = hcol+1;
						}
					}
				}
			}
			for(int w=0;w<v;w++)
			{
				printf("%d ",colorGraph[w]);
			}
			printf("\n");
		}
	}

	//Colored Graph
	int numCol = 0;
	for(i = 0; i < v; i++) 
	{
  		for (j=0; j<i; j++)
		{
      			if (colorGraph[i] == colorGraph[j])
      	 			break;
       		}
      		if (i == j)
      			numCol+=1;
  	}

	//Displaying number of colors required
	printf("Number of Colors Required :: %d\n",numCol);
	
	//Displaying the colored graph
	printf("Colored Graph :: \n");
	for(i=0;i<v;i++)
	{
		printf("%d ",colorGraph[i]);
	}
	printf("\n");
}
