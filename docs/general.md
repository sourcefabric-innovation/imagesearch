**Notices:**

* Data (for both requests and responses) transferred as json.

* The system should be able to have several separate indexes;
  requests (individually) specify which index to use.

* The index with tag-suggestion abilities should be a precreated one;
  we probably will not put our own images and tags into it, at least in the first iteration.

* To be able to start/stop the system with a standard system startup script;
  with possibility to set IP address and port to listen at.

* Regarding non-GET/POST methods, the system should allow
  the standard header substitution for the actual method type,
  i.e. via the X-HTTP-Method-Override header on the POST method.

* Regarding tags: may be to do it via (integer) Ids,
  so that we can put in some localization by ourselves (in an outer layer);
  otherwise we need to know how we can handle localization of tags.

* We should get a description how to make a deployment, backup and recovery.

* Return proper HTTP status codes for every request;
  i.e. on a failure, 40x status code should be returned, with reason phrase
  simply describing what got wrong.

