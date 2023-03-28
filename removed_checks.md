## Checks removed for EDT:
### Some checks were already removed in EMPI, which are not mentioned here
```
usend.c:
    OMPI_CHECK_DATATYPE_FOR_SEND(rc, type, count);
    OMPI_CHECK_USER_BUFFER(rc, buf, type, count);
    memchecker_call(&opal_memchecker_base_isdefined, buf, count, type); //not sure!!

urecv.c:
    OMPI_CHECK_DATATYPE_FOR_RECV(rc, type, count);
    OMPI_CHECK_USER_BUFFER(rc, buf, type, count);
    memchecker_call(&opal_memchecker_base_isaddressable, buf, count, type); //not sure!!

ubcast.c:
    memchecker_datatype(datatype);
    memchecker_call(&opal_memchecker_base_isdefined, buffer, count, datatype);
    OMPI_CHECK_DATATYPE_FOR_SEND(err, datatype, count);

uallreduce.c:
    memchecker_call(&opal_memchecker_base_isaddressable, recvbuf, count, datatype);
    memchecker_call(&opal_memchecker_base_isdefined, recvbuf, count, datatype);
    OMPI_CHECK_DATATYPE_FOR_SEND(err, datatype, count);

uallgather.c:
    ompi_datatype_type_extent(recvtype, &ext);
    memchecker_datatype(recvtype);
    memchecker_comm(comm);
    memchecker_datatype(sendtype);
    memchecker_call(&opal_memchecker_base_isdefined, sendbuf, sendcount, sendtype);
    memchecker_call(&opal_memchecker_base_isaddressable, recvbuf, recvcount, recvtype);
    if (MPI_DATATYPE_NULL == recvtype || NULL == recvtype) ...;
    if ( 0 == sendcount && 0 == recvcount ) 
	    return MPI_SUCCESS;
    


iusend.c:
    memchecker_call(&opal_memchecker_base_isdefined, buf, count, type);
    OMPI_CHECK_DATATYPE_FOR_SEND(rc, type, count);
    OMPI_CHECK_USER_BUFFER(rc, buf, type, count);

iurecv.c:
    OMPI_CHECK_DATATYPE_FOR_RECV(rc, type, count);
    OMPI_CHECK_USER_BUFFER(rc, buf, type, count);
    memchecker_call(&opal_memchecker_base_mem_noaccess, buf, count, type);

iubcast:
    memchecker_call(&opal_memchecker_base_isdefined, buffer, count, datatype);
    OMPI_CHECK_DATATYPE_FOR_SEND(err, datatype, count);


```