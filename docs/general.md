
Notices:

* data (for both requests and responses) transferred as json.

* the system should be able to have several separate indexes;
  requests (individually) specify which index to use.

* the index with tag-suggestion abilities should be a precreated one;
  we probably will not put our own images and tags into it, at least in the first iteration.

* to be able to start/stop the system with a standard system startup script;
  with possibility to set IP address and port to listen at.

* regarding non-GET/POST methods, the system should allow
  the standard header substitution for the actual method type,
  i.e. via the X-HTTP-Method-Override header on the POST method.

* regarding tags: may be to do it via (integer) Ids,
  so that we can put in some localization by ourselves (in an outer layer).

* we should get a description how to make a deployment, backup and recovery.

* on a failure, 40x status codes should be returned, with reason phrases
  simply describing what got wrong.


